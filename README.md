# AlphaOne Harness

**AI Coding Workbench powered by AlphaOne HyperRouter**

AlphaOne Harness is a Windows-native AI coding workbench designed for workspace-aware software development with agentic planning, code editing, build/test validation, diagnostics, change review, and controlled execution.

AlphaOne Harness uses **AlphaOne HyperRouter** as its AI connectivity layer. Provider credentials and model routing are managed by HyperRouter rather than directly inside AOH.

> Official public distribution repository for AlphaOne Harness binaries, release notes, and installation documentation.  
> The AlphaOne Harness source code is proprietary and is not distributed through this repository.

---

## Download

### Latest Release

Download the latest official Windows installer from:

**[Download AlphaOne Harness](../../releases/latest)**

All published versions are available on the:

**[Releases Page](../../releases)**

Each release includes its own version notes, compatibility information, and downloadable Windows installer.

---

## What is AlphaOne Harness?

AlphaOne Harness combines an IDE-style workbench with an AI development agent.

```text
Developer
   │
   ▼
AlphaOne Harness
   │
   ├── Workspace / Project Intelligence
   ├── AI Chat & Agent Workflow
   ├── Code Editing
   ├── Search / Replace
   ├── Terminal
   ├── Build / Test
   ├── Problems / Diagnostics
   ├── Git Review
   ├── AI Diff Review
   ├── Checkpoints / Undo / Redo
   └── Approval & Permissions
          │
          ▼
AlphaOne HyperRouter
          │
          ├── Cloud AI Providers
          ├── Local GGUF AI
          ├── Provider Routing
          ├── Auto RollOver
          └── Token / Quota Diagnostics
```

AOH focuses on the **development workflow**. HyperRouter focuses on **AI provider/model connectivity and routing**.

---

## Key Features

### Workspace-Aware Agentic Coding

AOH can work from the active workspace or solution without requiring the user to provide exact file paths for normal development tasks.

Typical workflow:

```text
Understand workspace
        ↓
Search relevant files
        ↓
Create implementation plan when appropriate
        ↓
Review / Proceed
        ↓
Edit code
        ↓
Build
        ↓
Diagnose failures
        ↓
Fix and rebuild
        ↓
Run tests
        ↓
Review resulting changes
        ↓
Final walkthrough
```

### Project & Solution Intelligence

AOH can discover and reason about common project structures and multi-project workspaces.

Supported project/build ecosystems include common workflows around:

- .NET
- Node.js / npm / pnpm / yarn / bun
- Python / pytest / Poetry
- Rust / Cargo
- Go
- Java / Gradle / Maven
- Flutter / Dart
- CMake
- Composer

Actual build/test capability depends on the tools installed for the active project.

### Integrated Code Workbench

AOH includes:

- Workspace Explorer
- Multi-document editor
- Find in Files
- Replace in Files
- File and folder operations
- Open File / Open Folder / Open Recent
- Auto Save with stale-write protection
- External-file editing through explicit user-selected file access

### Developer Console

Bottom-panel tooling includes:

- Trajectory
- Interactive Terminal
- Output
- Problems
- Runtime Logs

AOH also provides project-aware Build and Test workflows with truthful raw execution output and structured diagnostics where supported.

### AI Diff Review

Agent-produced changes can be reviewed independently from Git.

Capabilities include:

- Live Agent change review
- Per-change Accept
- Per-change Reject where safely supported
- Per-file review
- Added-file review
- Historical AI Diff Review
- Protection against stale or externally modified files

### Agent Checkpoints / Undo / Redo

AOH maintains bounded Agent change checkpoints for supported tracked edits.

This enables guarded workflows such as:

- Undo Agent turn
- Restore earlier Agent checkpoint
- Redo eligible undone work

These features are designed to protect current disk/editor state and do not use Git as an unconditional rollback mechanism.

### Implementation Plan & Progress

For larger coding tasks, AOH can present an implementation plan before execution.

The user can:

- Review the plan
- Add feedback
- Request revision
- Authorize implementation
- Follow structured progress
- Review the final work result

### Approval & Permissions

Agent actions are governed by configurable approval policy.

Categories include:

- Search files
- Read files
- Create files
- Edit files
- Delete files
- Run shell commands
- Network / Send data
- External / MCP tools

Available policy styles include:

- Strict
- Balanced
- Autonomous
- Custom

Unknown or unclassified tools fail toward review rather than silently gaining unrestricted authority.

---

## Powered by AlphaOne HyperRouter

AOH does not ask users to configure OpenAI, Google, Anthropic, DeepSeek, Qwen, or other provider API keys directly inside the AOH workbench.

AI connectivity is routed through:

```text
AlphaOne Harness
      │
      ▼
AlphaOne HyperRouter
      │
      ├── OpenAI-compatible gateway
      ├── Responses API compatibility
      ├── Cloud AI providers
      ├── Local GGUF AI
      ├── Auto RollOver
      └── Provider/model routing
```

Default HyperRouter endpoint:

```text
http://127.0.0.1:11436
```

AOH uses the stable public model identity:

```text
alphaone-hyperrouter
```

The physical provider/model selection remains owned by HyperRouter.

---

## Installation

### Windows Installer

Download:

```text
AlphaOne_Harness_Setup_v1.0.0.exe
```

from the latest GitHub Release.

The installer provides one integrated Windows installation experience.

### Prerequisite behavior

```text
AOH Setup
   │
   ├── Microsoft Edge WebView2 Runtime
   │      ├── already installed → reuse / skip
   │      └── missing           → run bundled Microsoft bootstrapper
   │
   ├── AlphaOne HyperRouter
   │      ├── compatible version installed → preserve
   │      ├── older version installed      → upgrade
   │      └── not installed                → install bundled HyperRouter
   │
   └── AlphaOne Harness
          → install application + production runtime
```

AOH and HyperRouter remain separate installed products with separate versioning and uninstall entries.

AOH uninstall does **not** remove HyperRouter or HyperRouter credentials/configuration.

> The AOH and HyperRouter application payloads are bundled in the AOH installer.  
> Microsoft runtime prerequisites may still require internet access if they are missing from the system.

---

## Quick Start

### 1. Install AlphaOne Harness

Download and run the latest:

```text
AlphaOne_Harness_Setup_v1.0.0.exe
```

The installer will verify required prerequisites.

### 2. Configure HyperRouter

Open the HyperRouter Settings page:

```text
http://127.0.0.1:11436/setting
```

Configure at least one supported cloud provider or enable a compatible Local GGUF model.

### 3. Start AlphaOne Harness

Launch **AlphaOne Harness** from the Desktop or Start Menu.

AOH will start its bundled local production runtime and connect to HyperRouter for AI inference.

### 4. Open a Workspace

Use:

```text
File > Open Folder...
```

Then start a new AI session and describe the coding task.

Example:

```text
Find the cause of the current build failure, fix it, rebuild the project,
run the relevant tests, and show me the resulting changes.
```

---

## Installation Locations

Default installation:

```text
C:\Program Files\AlphaOne AI\Harness
```

Default HyperRouter installation:

```text
C:\Program Files\AlphaOne AI\HyperRouter
```

AOH local desktop runtime normally listens on:

```text
http://127.0.0.1:11435
```

HyperRouter normally listens on:

```text
http://127.0.0.1:11436
```

Both are local-loopback services under the default configuration.

---

## System Requirements

- Windows x64
- Microsoft Edge WebView2 Runtime
- AlphaOne HyperRouter
- Network access for cloud AI providers
- Provider API key(s) when using cloud AI
- Optional compatible `.gguf` model for Local AI
- Project-specific build/test tools required by the workspace

The installer can provision supported missing prerequisites as described above.

Actual Local AI performance depends on model size, available RAM, GPU VRAM, and hardware acceleration support.

---

## Release History

Every public release is published through **GitHub Releases**.

Release pages should contain:

- AOH version
- Release date
- Bundled / minimum HyperRouter version
- Change summary
- Bug fixes
- Compatibility changes
- Installation notes
- SHA-256 checksum
- Downloadable Windows installer

See:

**[All Releases](../../releases)**

Older versions may remain available for reference and rollback where appropriate.

---

## Security

AlphaOne Harness is designed primarily as a local Windows development workbench.

AOH includes security boundaries for:

- Workspace containment
- Version-checked file mutation
- Agent approval policy
- Tool execution approval
- Sandbox-aware execution
- Exact-file user grants
- Stale/conflict protection
- Local runtime ownership and cleanup

Provider API credentials remain owned by **AlphaOne HyperRouter**.

Users remain responsible for:

- Protecting provider credentials
- Reviewing Agent changes before acceptance
- Reviewing approval prompts
- Protecting local source code and workspaces
- Downloading AOH only from official AlphaOne AI distribution channels
- Reviewing release notes before production use

---

## Official Website

**AlphaOne AI**

https://alphaone-ai.com

AlphaOne Harness product information:

https://alphaone-ai.com/

AlphaOne HyperRouter:

https://alphaone-ai.com/hyperrouter.html

---

## Support

For AlphaOne Harness questions, beta testing, compatibility reports, or release-related issues:

**support@alphaone-ai.com**

When reporting an issue, include where applicable:

- AlphaOne Harness version
- AlphaOne HyperRouter version
- Windows version
- Workspace / project type
- Relevant Build / Test output
- Relevant AOH runtime log information
- Relevant HyperRouter status information

Do **not** include API keys, credentials, private source code, or other secrets in public GitHub issues.

---

## Binary Distribution Notice

This repository is intended for:

- Official AlphaOne Harness release announcements
- Version history
- Release notes
- Installation documentation
- Public Windows binary downloads

It is **not** the AlphaOne Harness source-code repository.

Executable files published under the official **Releases** section are the intended public distribution artifacts.

---

## License & Intellectual Property

AlphaOne Harness is proprietary software.

Copyright © 2026 AlphaOne AI. All rights reserved.

The availability of downloadable binaries through this repository does not grant permission to reproduce, redistribute, reverse engineer, modify, sublicense, or commercially exploit AlphaOne-authored proprietary software except where expressly authorized by AlphaOne AI.

AlphaOne Harness includes third-party and open-source components distributed under their respective licenses. Applicable third-party rights and notices are preserved with the installed product.

Third-party product names, trademarks, APIs, and services remain the property of their respective owners.

AlphaOne AI is an independent third-party software provider and is not affiliated with, endorsed by, or sponsored by OpenAI, Anthropic, Google, DeepSeek, Alibaba Cloud, Moonshot AI, Microsoft, or other referenced technology providers.

---

**AlphaOne Harness**  
*Powered by AlphaOne HyperRouter*

**Plan. Build. Diagnose. Fix. Review.**
