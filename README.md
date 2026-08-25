# PluresLM Scout

PluresLM Scout connects [Microsoft Scout](https://learn.microsoft.com/copilot/) and compatible Copilot surfaces to a local-first PluresLM memory service. This repository is the public home for **released packages, installation guidance, release notes, and user support**.

## Where the code lives

The implementation and its CI live in the [Praxis Platform monorepo](https://github.com/plures/praxis-platform). The Scout adapter will be maintained there as `packages/plureslm-scout`, alongside the shared PluresLM service and its enforced store-ownership policy.

This repository deliberately contains no runtime source code, dependency lockfiles, or CI workflows. A release asset is published here only after the corresponding platform release workflow has produced and verified it.

## Downloads

No end-user release is available yet. When the first supported release is ready, download the Windows package from [Releases](https://github.com/plures/plureslm-scout/releases) and follow its version-specific installation notes.

## What it will provide

- Scout/Copilot prompt-time recall through the PluresLM service.
- A supported installer and upgrade path for Windows.
- An optional MCP configuration for Scout/Copilot tools.

The shared PluresLM service remains the only owner of a shared live memory store. The Scout integration is a client: it must not open the service's database path directly or silently fall back to a separate shared-store implementation.

## Support

Use this repository for installation, compatibility, and release-support issues. Please include the release version, Windows version, Scout/Copilot host version, and non-sensitive logs. Do not include memory contents, database files, access tokens, or other credentials.

See [release publishing](docs/RELEASING.md) and [support boundaries](docs/SUPPORT.md) for details.

## Related projects

- [PluresLM](https://github.com/plures/pluresLM) — local-first memory foundation.
- [Praxis Platform](https://github.com/plures/praxis-platform) — canonical source and CI.
- [OpenClaw](https://github.com/plures/openclaw) — a separate host integration.
