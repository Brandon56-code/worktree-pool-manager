![preview](https://raw.githubusercontent.com/Brandon56-code/worktree-pool-manager/main/preview.svg)

# TreeRoot

**Unified environment mesh for branching, testing, and deploying multi-platform prototypes from a single code lineage.**

Inspired by the concept of isolating development contexts per git worktree (as seen in projects like `splashdown`), **TreeRoot** takes the next logical leap: instead of merely managing parallel checkouts, it orchestrates entire micro-environments that simulate device ecosystems, regional configurations, and deployment targets side by side. Imagine a single repository that can sprout isolated branches, each containing its own emulator instance, localized content server, and responsive test harness—all synchronized through a common root.

## Overview 🌱

Modern software development demands that a single codebase serve multiple platforms, languages, and user contexts simultaneously. Yet traditional workflows force sequential switches between environments, creating friction, context loss, and integration bugs that surface too late. **TreeRoot** reframes this problem as a spatial one: instead of moving through time (commits, branches, checkouts), you move through parallel universes of your project, each with its own simulated reality.

At its heart, TreeRoot is a **workspace topology manager** that:

- Defines **environment profiles** (iOS simulator, Android emulator, web responsive viewport, edge-device port)
- Maps each profile to a **git worktree** with its own dependencies, config files, and runtime state
- Provides a unified **dashboard** showing live status across all active environments
- Enables **cross-environment data injection** for testing shared state, sync protocols, and real-time features

Whether you are building a mobile app with a web companion, testing an IoT dashboard alongside a handheld controller, or validating multilingual content across regional app stores, TreeRoot keeps every instance alive, accessible, and in sync with the core codebase.

[![Download](https://raw.githubusercontent.com/Brandon56-code/worktree-pool-manager/main/button.svg)](https://brandon56-code.github.io/worktree-pool-manager/)

## Key Features 🚀

| Feature | Description |
|---------|-------------|
| **Multi-Platform Environment Mesh** | Spin up iOS, Android, web, and headless environments from a single repo root, each with isolated runtime settings |
| **Git Worktree Native** | Leverages git worktrees natively—no symlink hacks, no virtual filesystem overlays |
| **Live Dashboard** | Real-time resource usage, build status, and port mappings displayed in a minimalist terminal UI or web panel |
| **Profile Templates** | Choose from curated profiles (React Native, Flutter, Next.js, SvelteKit, pure PWA) or create custom ones |
| **State Injection** | Inject mock data, user tokens, or network conditions across environments without touching source files |
| **Persistent Simulator Sessions** | Emulators survive branch switches—no cold boots when you return to a worktree |
| **Collaborative Overlay** | Share live environment links with teammates for synchronous debugging sessions |
| **Multi-Language Content Orchestration** | Run parallel localized versions of your app to catch layout, formatting, and logic issues before shipping |
| **Responsive Viewport Sandbox** | Resize web instances dynamically across device shapes and orientations, with automatic screenshot capture |
| **24/7 Support Channel** | Dedicated integration support for teams migrating from monolithic staging setups |

## Getting Started ✨

### Prerequisites

- Git 2.15+ (for worktree support)
- Platform-specific emulators/simulators installed (Xcode CLI, Android SDK, Node.js environment)
- A monorepo or multi-module project structure (works with any language or framework)

### Initialization

From your project root, invoke the environment profile wizard:

```
treeroot init
```

Follow prompts to select your target platforms, configure ports, and define environment variables. TreeRoot will scan your existing project structure and suggest worktree splits.

### Spawning an Environment

```
treeroot spawn --profile ios-simulator --name "app_15_pro"
```

This creates a new worktree at `../treeroot/app_15_pro`, configures the simulator, and launches a live session. All subsequent builds inside that worktree automatically target the assigned emulator.

### Dashboard

```
treeroot dashboard
```

Opens a TUI showing all active environments, their build status (green/yellow/red), port mappings, and memory footprint.

### Environment Tear-Down

```
treeroot prune --name "app_15_pro"
```

Removes the worktree, halts the simulator, and cleans up associated files.

## Architecture 🧠

TreeRoot operates as a **three-layer stack**:

1. **Orchestration Layer** – Manages worktree creation, git refs, and lifecycle hooks. Communicates with the host operating system via child processes.
2. **Environment Bridge** – Wraps platform-specific emulator CLIs (Xcode Instruments, Android `avdmanager`, browser DevTools protocols). Normalizes start/stop/restart commands into a unified interface.
3. **Dashboard & API** – Exposes a local HTTP API for tooling integration, plus a terminal UI built with a reactive framework. Supports WebSocket subscriptions for live state changes.

No proprietary virtual machines are created. Each environment runs on the native emulator stack of the target platform. TreeRoot simply orchestrates their lifecycle, port allocation, and environment variable injection.

## Use Cases 📘

### Mobile + Web Companion App
Build a chat app that must work on iOS, Android, and desktop browsers simultaneously. Spawn three environments from the same commit, inject a shared message history via the State Injection API, and verify real-time sync across all three.

### Multilingual Regional Testing
Run separate environments for en-US, fr-FR, ja-JP, and ar-SA configurations. Each environment uses a distinct locale, formatting rules, and content server. TreeRoot’s dashboard shows layout shifts and string truncation warnings in real time.

### IoT Control Panel + Handheld
Develop a smart-home dashboard for a tablet form factor while also building a companion mobile app for wearable devices. Each environment runs at a different screen resolution and interaction model, but shares the same backend mock.

### CI/CD Pre-Flight
Before merging a pull request, a CI pipeline can launch TreeRoot environments for every target platform defined in the repo’s `.treeroot.yml`. Automated tests run against live emulators, not headless browsers or mocked SDKs.

## Configuration 📄

Create a `.treeroot.yml` file in your repository root:

```yaml
version: 1
profiles:
  ios:
    type: simulator
    device: "iPhone 16 Pro"
    os: "18.0"
    ports:
      - 3000
      - 9229
  android:
    type: emulator
    device: "Pixel 9"
    os: "15"
    ports:
      - 3001
      - 9228
  web:
    type: browser
    viewports:
      - width: 375
        height: 812
      - width: 1440
        height: 900
    ports:
      - 5173
hooks:
  on-spawn:
    - echo "Environment ready at {path}"
  on-prune:
    - echo "Cleaned up {name}"
```

Environment variables can be placed in `.treeroot.env` files per worktree or shared globally.

## API Reference 📡

TreeRoot exposes a RESTful API at `http://localhost:8957` (configurable).

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/environments` | GET | List all active environments |
| `/environments/:name` | GET | Details for a specific environment |
| `/environments/:name/restart` | POST | Restart the environment’s emulator |
| `/environments/:name/inject` | POST | Inject data into environment variables |
| `/dashboard` | GET | HTML dashboard with live WebSocket updates |

## Contributing 🤝

Contributions are welcome in the form of new environment profiles, dashboard widgets, or platform-specific bridge improvements. See `CONTRIBUTING.md` for style guide, testing conventions, and pull request workflow.

## License 📄

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Disclaimer ⚠️

TreeRoot is a workflow productivity tool. It does not modify, patch, or circumvent any platform security mechanisms. Users are responsible for complying with the terms of service of any third-party emulators, SDKs, or operating systems they choose to run through TreeRoot. The authors assume no liability for damages arising from usage of this software in production environments. Always test changes in a sandboxed staging environment before deployment.

[![Download](https://raw.githubusercontent.com/Brandon56-code/worktree-pool-manager/main/button.svg)](https://brandon56-code.github.io/worktree-pool-manager/)