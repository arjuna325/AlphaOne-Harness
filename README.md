# AlphaOne Harness

**AI Coding Workbench powered by AlphaOne HyperRouter**

AlphaOne Harness (AOH) is a Windows AI coding workbench. It combines a full code editor with an AI agent that plans, edits, builds, tests, and reviews work in your project.

AOH uses **AlphaOne HyperRouter** as its only AI backend. Provider credentials and model routing stay in HyperRouter, not in AOH.

> This is the official public distribution repository for AlphaOne Harness installers, release notes, and installation documentation.
> The AlphaOne Harness source code is proprietary and is not distributed through this repository.

---

## Download

**[Download the latest AlphaOne Harness](../../releases/latest)**

All published versions are on the **[Releases page](../../releases)**. Each release has its own notes, the Windows installer, and an `aoh-update.json` file that AOH uses to update itself.

---

## What Is New in Version 2

AlphaOne Harness 2 is a new workbench built on Code - OSS, the open-source editor behind Visual Studio Code. It replaces AlphaOne Harness 1.

- A full editor with Explorer, Search, Terminal, Problems, Git, debugging, and extensions from Open VSX
- An AI agent with Implementation Plans, progress tracking, and a final walkthrough
- Scheduled tasks that run the agent on a timetable
- Access from your phone through Telegram and Email
- Automatic updates through GitHub Releases

---

## Architecture

```text
Developer (PC, or phone through Telegram / Email)
   │
   ▼
AlphaOne Harness
   │
   ├── Editor, Explorer, Search, Terminal, Git
   ├── AI Agent (Agent, Plan, and Ask modes)
   ├── Implementation Plan, Progress, Walkthrough
   ├── Build / Test / Fix loop
   ├── Keep / Undo review and checkpoints
   ├── Scheduled Tasks
   └── Connections (Telegram, Email, Tavily web search)
          │
          ▼
AlphaOne HyperRouter  (http://127.0.0.1:11436)
          │
          ├── Cloud AI providers
          ├── Local GGUF models
          ├── Provider and model routing
          └── Embeddings for semantic search
```

AOH focuses on the development workflow. HyperRouter focuses on AI provider and model connectivity.

---

## Key Features

### AI Agent

Describe a task in chat. The agent searches the workspace, edits files, runs commands, and reports what it did.

- **Agent, Plan, and Ask modes.**
- **Implementation Plan:** for larger tasks the agent writes a plan that opens in the editor. You can comment on it, ask for a revision, or click **Proceed**.
- **Progress:** after Proceed, the agent tracks a to-do list based on what it has actually done.
- **Final Walkthrough:** a summary of the changes and how they were verified.
- **Build / Test / Fix loop:** the agent builds, reads the errors, fixes them, and runs the tests again.
- **Run and test projects:** the agent can start a web project, check it in the built-in browser with screenshots, and close it afterwards.

### Review and Undo

- Files edited by the agent open in the editor at the change.
- Each change can be kept or undone with **Keep** and **Undo**.
- Checkpoints let you return to an earlier point of the chat session.

### Project Search

- Text and file search across the workspace.
- **Repo Map:** finds functions, classes, and types by name, without embeddings.
- **Semantic search** and a project Knowledge Base, using embeddings from HyperRouter.
- **Explore** subagent for longer searches.

### Documents and the Web

- **read_document** reads PDF, DOCX, and XLSX files.
- **Web search** through Tavily when a Tavily API key is set in AOH Connections.

### Memory and Skills

- **Long-term memory:** the agent records project facts and your preferences, and uses them in later sessions.
- **Skills:** reusable instructions in `SKILL.md` files. After a complex task, the agent can suggest a new skill or an update, with your approval.

### Scheduled Tasks

Run an agent task on a schedule, such as every day at 07:00.

- Cron-style schedule form, run history, and **Run Now**.
- Each task runs in its own project, in a minimized window.
- Runs missed while AOH was closed can run when it starts again.
- **Ask Before Each Run** and approvals can be sent to Telegram or Email. Results are sent there too.
- A **Stop** button ends a running task.

### Phone Access (Telegram and Email)

Send a task from your phone while AOH is open on your PC, and get the answer back in the same app.

- Only allowed senders can use it, added with a pairing code.
- Risky actions need your approval from the phone with `/approve` or `/deny`.
- Commands: `/new`, `/status`, `/stop`, `/approve`, `/deny`, `/help`.
- All settings, including the Tavily key, are entered in the **AOH Connections** form. Secrets are kept in the Windows secret storage.

### Approvals and Permissions

Tool calls such as editing files, running terminal commands, and sending data follow the approval settings of the workbench. Commands that need approval wait for you, on the PC or on the phone.

### Extensions

Extensions can be installed from **Open VSX** in the Extensions view.

### Automatic Updates

AOH checks GitHub Releases for a newer version. It downloads the installer, checks its SHA-256 hash, and installs it when you click **Restart to Update**.

---

## Powered by AlphaOne HyperRouter

You do not enter OpenAI, Google, Anthropic, DeepSeek, Qwen, or other provider API keys in AOH. AOH sends every AI request to HyperRouter.

- Default endpoint: `http://127.0.0.1:11436`
- Model name used by AOH: `alphaone-hyperrouter`

The actual provider and model are chosen by HyperRouter.

---

## Installation

Download `AlphaOne_Harness_Setup_v<version>.exe` from the latest release and run it. The installer needs administrator rights, because it installs for all users.

```text
AOH Setup
   │
   ├── AlphaOne Harness 1 found?
   │      └── yes → uninstalled first
   │
   ├── AlphaOne Harness 2
   │      → installed to C:\Program Files\AlphaOne AI\Harness
   │
   └── AlphaOne HyperRouter
          ├── not installed           → bundled installer runs
          ├── older version installed → bundled installer upgrades it
          └── same or newer version   → skipped
```

AOH and HyperRouter are separate products, with separate versions and uninstall entries. Uninstalling AOH does not remove HyperRouter or its settings.

> **Upgrading from version 1:** the uninstaller of version 1 also removes the data of version 1. Version 2 keeps its own data in `%APPDATA%\AlphaOne Harness`.

---

## Quick Start

1. **Install** AlphaOne Harness with the latest installer.
2. **Configure HyperRouter** at `http://127.0.0.1:11436/setting`. Add at least one cloud provider or enable a local GGUF model.
3. **Start AlphaOne Harness** from the Desktop or Start Menu.
4. **Open a project** with **File > Open Folder...**, then describe a task in chat. For example:

```text
Find the cause of the current build failure, fix it, rebuild the project,
run the relevant tests, and show me the changes.
```

5. Optional: open **AOH Connections** to add a Tavily key for web search, or to connect Telegram and Email.

---

## System Requirements

- Windows 10 or 11, x64
- AlphaOne HyperRouter (bundled with the installer)
- Internet access for cloud AI providers, web search, Telegram, and Email
- Provider API keys in HyperRouter when you use cloud AI
- Optional: a compatible `.gguf` model for local AI
- The build and test tools that your project needs, such as .NET, Node.js, Python, or Java

Local AI performance depends on the model size, RAM, GPU VRAM, and hardware acceleration.

---

## Security

- The agent works inside the opened workspace. Edits can be reviewed with Keep and Undo.
- Terminal commands and other risky tools follow the approval settings.
- Phone access only accepts allowed senders, and messages older than 10 minutes are not run.
- API keys, bot tokens, and email passwords are kept in the Windows secret storage, not in settings files.
- Provider credentials stay in AlphaOne HyperRouter.

You remain responsible for:

- Protecting your provider credentials, bot tokens, and email passwords
- Reviewing agent changes and approval requests
- Downloading AOH only from official AlphaOne AI channels
- Reading the release notes before production use

The installer is not code-signed yet, so Windows SmartScreen may show a warning. Check that the SHA-256 hash in `aoh-update.json` matches the installer you downloaded.

---

## Official Website

- AlphaOne AI: https://alphaone-ai.com
- AlphaOne HyperRouter: https://alphaone-ai.com/hyperrouter.html

---

## Support

For questions, beta testing, compatibility reports, or release issues: **support@alphaone-ai.com**

When you report an issue, include where possible:

- AlphaOne Harness version (Help > About)
- AlphaOne HyperRouter version
- Windows version
- Project type
- The relevant build or test output and error messages

Do **not** include API keys, tokens, passwords, private source code, or other secrets in public GitHub issues.

---

## License and Intellectual Property

AlphaOne Harness is proprietary software.

Copyright © 2026 AlphaOne AI. All rights reserved.

Downloadable installers in this repository do not grant permission to reproduce, redistribute, reverse engineer, modify, sublicense, or commercially exploit AlphaOne software, except where AlphaOne AI expressly authorizes it.

AlphaOne Harness is built on Code - OSS and includes other open-source components under their own licenses, including the MIT License. Their notices are installed with the product.

Visual Studio Code is a trademark of Microsoft Corporation. Third-party product names, trademarks, APIs, and services belong to their owners. AlphaOne AI is an independent software provider and is not affiliated with, endorsed by, or sponsored by Microsoft, OpenAI, Anthropic, Google, DeepSeek, Alibaba Cloud, Moonshot AI, Telegram, or other referenced technology providers.
**AlphaOne Harness**  
*Powered by AlphaOne HyperRouter*

**Plan. Build. Diagnose. Fix. Review.**
