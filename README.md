# PluresLM Scout

PluresLM Scout connects [Microsoft Scout](https://learn.microsoft.com/copilot/) and compatible Copilot surfaces to the local-first **PluresLM Desktop Broker**. This repository is the public home for **released packages, installation guidance, release notes, and user support**.

## Where the code lives

The implementation and its CI live in the [Praxis Platform monorepo](https://github.com/plures/praxis-platform). The Scout adapter will be maintained there as `packages/plureslm-scout`, alongside the shared PluresLM service and its enforced store-ownership policy.

This repository deliberately contains no runtime source code, dependency lockfiles, or CI workflows. A legacy compatibility release asset is published here only after the corresponding platform release workflow has produced and verified it.

## Downloads

Existing Scout-branded Windows ZIPs are available from
[Releases](https://github.com/plures/plureslm-scout/releases). They are legacy
compatibility packages, not the unified PluresLM product installer. Follow the
selected release's installation notes and verify its matching SHA-256 file.

PluresLM's direction is **one product installer per operating-system/architecture
target**, starting with the Windows x64 MSI. Scout, Copilot, Codex, VS Code,
and OpenClaw are optional integrations of the same broker, not separate
PluresLM installations or release channels. The canonical source is Praxis
Platform; the product distribution mirror is
[plures/pluresLM](https://github.com/plures/pluresLM/releases). That repository
may require access; a missing or inaccessible release is not proof of an
available product installer.

The MSI does not yet automatically configure Scout hooks or migrate a legacy
Scout installation. Do not delete existing memory or credentials, silently
repoint clients, or run competing broker processes against the same store.
The [platform operating model](https://github.com/plures/praxis-platform/blob/main/docs/PLURESLM-PROJECT-OPERATING-MODEL.md)
records the remaining integration and migration gates.

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
