##### Examples

List shared mounts or a folder on a dial-book phone. Bare `phone-…` lists mounts; a path lists that folder. Quote globs.

```sh
tanit-cli node ls phone-0e404e231f39ff6c
tanit-cli node ls phone-0e404e231f39ff6c --json
tanit-cli node ls vfs://phone-0e404e231f39ff6c/pictures --json
tanit-cli node ls vfs://phone-0e404e231f39ff6c/dcim/Camera --glob "*.jpg"
```

Plan a backup without writing by combining `ls` with `cp --dry-run` (see `cp` examples).
