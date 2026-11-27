##### Examples

`cp` and `copy` copy through the same queue as the file panel. The last path is the destination folder unless `--dst` is set. Quote globs and any URI that contains a space. A finished copy emits each destination path as a run artifact.

`${CWD}`, `${ENV:…}`, `${KNOWNFOLDER:Desktop}`, and `${SRC_NAME}` expand in `--src` and `--dst`.

On **PowerShell**, single-quote Tanit `${…}` tokens (or use `--dst '…'`). Double-quoted `"${KNOWNFOLDER:Desktop}"` is eaten by PowerShell as a drive-scoped variable and the dest vanishes, which surfaces as `missing source`.

**Local folder**

```sh
tanit-cli cp report.pdf notes.md ./out
tanit-cli cp "shots/*.{jpg,png}" --dst '${KNOWNFOLDER:Desktop}'
```

**Preview, then copy**

```sh
tanit-cli cp report.pdf ./out --dry-run
tanit-cli cp report.pdf ./out --if-newer --json
```

**SSH / SFTP** (`ssh://host/` is the filesystem root; a host with no slash opens that session's home. A key in `~/.ssh` is used when the URI has no password.)

```sh
tanit-cli cp report.pdf ssh://workshop/opt/incoming
tanit-cli cp ssh://workshop/home/you/readme.md ./inbox
tanit-cli cp ./build sftp://user:password@host/var/drops --overwrite
```

**FTP / FTPS**

```sh
tanit-cli cp report.pdf ftp://user:password@host/pub
tanit-cli cp ftps://user@host/inbox/brief.pdf ./inbox --skip
```

**Tanit VFS** (`vfs://{mount}/{path}` — `home`, `models`, `software`, …)

```sh
tanit-cli cp diagram.png vfs://home/public
tanit-cli cp vfs://models/weights/model.gguf ./models --if-newer
```

**Phone or camera (MTP)** (folder names come from the device)

```sh
tanit-cli cp "mtp://realme/Internal storage/DCIM/IMG.jpg" ./inbox
tanit-cli cp shot.jpg "mtp://realme/Internal storage/DCIM"
```

Copy a phone file to a local folder, then copy that folder to SSH, FTP, or VFS. One command cannot put the phone on one side and SSH, FTP, or VFS on the other.

**Phone shared folders (`vfs://phone-…`)** — dial-book peer from `node peers`. Discover mounts with `node ls`, then copy. Put include/exclude globs on flags, not in the URI (`vfs://…/*.jpg` is not expanded on the phone).

###### Full backup (whole mount)

```sh
tanit-cli node peers --json
tanit-cli node ls phone-0e404e231f39ff6c --json
tanit-cli cp --dry-run --json --dst '${KNOWNFOLDER:Desktop}/phone-backup/pictures' vfs://phone-0e404e231f39ff6c/pictures
tanit-cli cp --dst '${KNOWNFOLDER:Desktop}/phone-backup/pictures' vfs://phone-0e404e231f39ff6c/pictures
tanit-cli cp --dst '${KNOWNFOLDER:Desktop}/phone-backup/dcim' vfs://phone-0e404e231f39ff6c/dcim
```

###### Partial backup (include / exclude)

```sh
tanit-cli node ls vfs://phone-0e404e231f39ff6c/dcim/Camera --glob "*.{jpg,jpeg,png,mp4}" --json
tanit-cli cp --dst '${KNOWNFOLDER:Desktop}/phone-photos' vfs://phone-0e404e231f39ff6c/dcim/Camera --include "*.jpg" --include "*.jpeg" --include "*.png" --include "*.mp4" --exclude "*.tmp"
```

###### Incremental backup (auto conflict)

Default conflict policy is `error`: a second run stops on the first file that already exists. Pick an auto strategy so re-runs only pull what you want. Convenience flags (`--if-newer`, `--skip`, …) are aliases of `--conflict …`.

Preview what would change, then sync only newer sources (usual daily backup):

```sh
tanit-cli cp --dry-run --json --if-newer --dst '${KNOWNFOLDER:Desktop}/phone-backup/dcim' vfs://phone-0e404e231f39ff6c/dcim
tanit-cli cp --if-newer --dst '${KNOWNFOLDER:Desktop}/phone-backup/dcim' vfs://phone-0e404e231f39ff6c/dcim
tanit-cli cp --conflict if-newer --include "*.jpg" --include "*.mp4" --dst '${KNOWNFOLDER:Desktop}/phone-photos' vfs://phone-0e404e231f39ff6c/dcim/Camera
```

Fill gaps without ever overwriting an existing dest (new camera rolls only):

```sh
tanit-cli cp --skip --dst '${KNOWNFOLDER:Desktop}/phone-backup/pictures' vfs://phone-0e404e231f39ff6c/pictures
```

Resume a truncated **local** dest after an interrupted pull (`reget` / `resume` continues from dest size when the source is larger; `append` keeps dest bytes and writes the full source after them). Neither applies to remote destinations:

```sh
tanit-cli cp --conflict reget --include "*.mp4" --dst '${KNOWNFOLDER:Desktop}/phone-videos' vfs://phone-0e404e231f39ff6c/dcim/Camera
tanit-cli cp --conflict append --dst '${KNOWNFOLDER:Desktop}/phone-videos' vfs://phone-0e404e231f39ff6c/dcim/Camera/VID_001.mp4
```

Clobber or keep a sibling name when you intentionally want that:

```sh
tanit-cli cp --overwrite --dst '${KNOWNFOLDER:Desktop}/phone-backup/dcim' vfs://phone-0e404e231f39ff6c/dcim
tanit-cli cp --rename --dst '${KNOWNFOLDER:Desktop}/phone-backup/dcim' vfs://phone-0e404e231f39ff6c/dcim
```

###### Interactive progress (`--ui`)

FTXUI TTY: batch + current-file gauges, speed, Esc / Ctrl+C cancel. Needs an interactive terminal. Plain `--ui` (default conflict `error`) opens Manual prompts. With an auto strategy (`--if-newer`, `--skip`, `--conflict reget`, …) the UI stays Auto — progress only, no mid-scan Manual park.

```sh
tanit-cli cp --ui --if-newer --dst '${KNOWNFOLDER:Desktop}/phone-backup/pictures' vfs://phone-0e404e231f39ff6c/pictures
tanit-cli cp --ui --conflict reget --include "*.mp4" --dst '${KNOWNFOLDER:Desktop}/phone-videos' vfs://phone-0e404e231f39ff6c/dcim/Camera
tanit-cli cp --ui --include "*.jpg" --dst '${KNOWNFOLDER:Desktop}/phone-photos' vfs://phone-0e404e231f39ff6c/dcim/Camera
```

**Keep or drop names**

```sh
tanit-cli cp ./photos --dst ssh://workshop/opt/incoming --include "*.jpg" --exclude "*~"
```
