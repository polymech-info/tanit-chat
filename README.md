# Tanit Chat

**A compact native Windows workspace for files, AI, and automation.**

Browse local and remote files, preview them beside chat, and put AI to work on your selection. Use local models, cloud providers, or both—with control over which tools they can use and where your data goes.

Tanit combines a file manager, media tools, an AI assistant, and visual automation in one C++ application. Optional CMS integration lets you publish directly from the workspace, while the Chrome extension connects browser pages with your files and native tools.

[Microsoft Store](https://apps.microsoft.com/detail/9n5f39064npd) · [Releases](https://github.com/polymech-info/tanit-chat/releases) · [Documentation](https://tanit.polymech.info/user/cgo/pages/documentation) · [CLI](https://tanit.polymech.info/user/cgo/pages/tanit-cli) · [Screenshots](./docs/screenshots.md)

---

## Why Tanit?

- **Native and compact** — a C++ core handles tools, security, and local inference through llama.cpp, whisper.cpp, and ONNX. The interface uses the operating system’s WebView.
- **Self-contained deployment** — no separate Node.js or Python installation required for the core application.
- **AI where you work** — ask questions about selected files, transform media, extract information, or automate a folder without leaving the workspace.
- **Local and cloud models** — keep processing on your machine or use approved providers, with model and tool access governed by presets and policy.
- **One agent across interfaces** — use the same capabilities through Chat, the CLI, and XBlox visual workflows.
- **Managed environments** — deployment options for schools, universities, and companies include GPO/Intune hooks, restricted interfaces, and shared model hosting on the LAN.

Start with a file and a request. Turn repeatable tasks into a preset or workflow when you need them again.

> Availability varies by edition, installed components, and organization policy.

---

## Features

| Area | Capabilities | Details |
|:-----|:-------------|:--------|
| **AI** | Local and cloud models, presets, MCP, planning, and voice | [AI](./docs/features/feature-ai.md) |
| **Files** | Local files, SSH, FTP, MTP, search, disk usage, and actions on selected files | [Files](./docs/features/feature-files.md) |
| **Images** | Culling, duplicate detection, EXIF/IPTC/XMP metadata, OCR, resizing, generation, and editing | [Images](./docs/features/feature-images.md) |
| **Audio** | Recording, local and cloud speech recognition and synthesis, voice commands, and realtime voice | [Audio](./docs/features/feature-audio.md) |
| **Video** | Screen, window, and camera capture; playback, captions, and silence skipping | [Video](./docs/features/feature-video.md) |
| **3D & CAD** | In-place previews for meshes, STEP/IGES, SolidWorks, FreeCAD, and OpenSCAD | [3D & CAD](./docs/features/feature-3d.md) |
| **Markdown** | Local documents with Mermaid diagrams, math, citations, callouts, and embedded media | [Markdown](./docs/features/feature-markdown.md) |
| **Automation** | XBlox visual workflows connecting files, applications, devices, media, and HTTP services | [Automation](./docs/features/feature-automation.md) |
| **CMS** | Publish reports, posts, images, and files directly from the workspace | [CMS](./docs/features/feature-cms.md) |
| **Chrome** | Research, translation, form filling, and workflows alongside the current page | [Chrome](./docs/features/feature-chrome.md) |
| **Security** | Encrypted settings, signing, agent gateway, sandbox controls, and backup | [Security](./docs/features/feature-security.md) |
| **Deployment** | Configure the interface, providers, tools, and policies for organizations, partners, MSPs, and OEMs | [Integration](./docs/features/feature-integration.md) |

For a comparison with coding agents and model runtimes—including Codex, Claude, Cursor, Ollama, Hermes, and Unsloth—see [Why Tanit](./docs/features/compare.md).

---

## Download

| Channel | Distribution |
|:--------|:-------------|
| [**Microsoft Store**](https://apps.microsoft.com/detail/9n5f39064npd) | Install Tanit and receive updates through the Store |
| [**GitHub Releases**](https://github.com/polymech-info/tanit-chat/releases) | Download available installers and portable builds |

Open a folder, select a file, and start a conversation. For recurring jobs, use a preset or build an XBlox workflow.

---

## Documentation

Browse the [feature guides](./docs/features/) or the [documentation mirrored in this repository](./docs/).

Online documentation:

- [Documentation overview](https://tanit.polymech.info/user/cgo/pages/documentation)
- [Tanit Chat](https://tanit.polymech.info/user/cgo/pages/tanit-chat-next)
- [CLI](https://tanit.polymech.info/user/cgo/pages/tanit-cli)
- [Command reference](https://tanit.polymech.info/user