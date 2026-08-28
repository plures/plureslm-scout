# PluresLM Scout

PluresLM Scout connects [Microsoft Scout](https://learn.microsoft.com/copilot/) and compatible Copilot surfaces to the local-first **PluresLM Desktop Broker**. This repository is the public home for **released packages, installation guidance, release notes, and user support**.

## Where the code lives

The implementation and its CI live in the [Praxis Platform monorepo](https://github.com/plures/praxis-platform). The Scout adapter will be maintained there as `packages/plureslm-scout`, alongside the shared PluresLM service and its enforced store-ownership policy.

This repository deliberately contains no runtime source code, dependency lockfiles, or CI workflows. A release asset is published here only after the corresponding platform release workflow has produced and verified it.

## Downloads

No end-user release is available yet. When the first supported release is ready, download the Windows package from [Releases](https://github.com/plures/plureslm-scout/releases) and follow its version-specific installation notes.

## What it will provide

- Scout/Copilot prompt-time recall and conservative explicit-request auto-stash through the PluresLM Desktop Broker.
- A supported installer and upgrade path for Windows.
- A service-backed MCP configuration for Scout/Copilot and Codex.

The Desktop Broker remains the only owner of a shared live memory store. Scout, OpenClaw, VS Code, Copilot, and Codex are clients: they must not open the database path directly or silently fall back to a separate store.

## Memory profiles and client support

The default installer profile is **unified**: Scout, generic MCP tools, and Codex share the user's `personal` memory space. Use `-MemoryProfile split` at installation when those clients should start with separate spaces. Every client receives an independent local capability and can access only its configured space.

The installer configures the local `plureslm` MCP bridge for Scout/Copilot. When Codex is installed, it also configures the same bridge for Codex CLI, the Codex IDE extension, and the ChatGPT desktop app. All of these local clients use the same broker, not separate databases.

ChatGPT on the web and ChatGPT Work do not read a local computer's MCP configuration. They require a separate, opt-in remote MCP/plugin deployment with HTTPS and OAuth; the Windows installer never exposes local memory remotely.

Auto-stash defaults to explicit user requests (`remember this`, `note:`, or `important:`). This avoids retaining ordinary prompts by default. The broker still applies its memory-admission policy before anything is stored.

## Support

Use this repository for installation, compatibility, and release-support issues. Please include the release version, Windows version, Scout/Copilot host version, and non-sensitive logs. Do not include memory contents, database files, access tokens, or other credentials.

See [release publishing](docs/RELEASING.md) and [support boundaries](docs/SUPPORT.md) for details.

## Related projects

- [PluresLM](https://github.com/plures/pluresLM) — local-first memory foundation.
- [Praxis Platform](https://github.com/plures/praxis-platform) — canonical source and CI.
- [OpenClaw](https://github.com/plures/openclaw) — a separate host integration.
