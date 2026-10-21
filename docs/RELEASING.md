# Release publishing

This repository is a release distribution and support surface. It does not build release artifacts.

## Source of truth

The Scout adapter, its tests, and release-generation workflow live in the Praxis Platform monorepo. A public release is published here only after that workflow has produced a versioned artifact and retained its verification evidence.

## Unified product boundary

PluresLM ships one product installer per supported OS/architecture target,
starting with the Windows x64 MSI. Harness adapters are optional components
of the same product and single broker, not independent installer products.
Canonical product releases belong to `plures/praxis-platform`, with identical
assets mirrored to `plures/pluresLM`.

This repository retains existing Scout ZIPs for compatibility. It is not a
second product-installer channel. The platform workflow continues to validate
Scout candidates, but publishing a legacy ZIP requires an explicit dispatch
on platform `main` with `publish_legacy_scout=true`. A normal push or dispatch
without that flag must not publish. This workflow change must be merged in
Praxis Platform before that behavior is effective.

The current MSI's shared broker and service-only MCP command are not proof
of automatic harness setup or migration. Do not claim those features until
their integration/upgrade tests pass.

## Release tags and recovery

The active `PluresLM immutable release tags` ruleset permits new `v*` and
`plureslm-v*` tags but prohibits updating or deleting them, with no bypass
actors. It does not grant repository write permission or replace artifact,
version, checksum, approval, or source-identity validation. Release assets
must never be overwritten merely because tag creation is allowed.

If a version belongs to an older platform commit, retain it. Prepare the next
reviewed component version rather than moving its tag or replacing its assets.
The platform's protected release environment and product-mirror credential
are separate prerequisites for the unified installer; the legacy Scout
publisher credential does not establish readiness for that channel.

## Publication requirements

Before publishing an artifact here, the platform release must provide:

- the immutable source revision and package version;
- the release artifact and SHA-256 checksum;
- platform validation evidence for the supported installer;
- release notes that identify compatibility requirements and upgrade guidance.

Do not rebuild, alter, or re-sign an artifact in this repository. The published checksum must describe the exact artifact generated and validated by the platform workflow.

## Release contents

Each release should include the installer or archive, a checksum file, concise installation instructions, a compatibility note for Scout/Copilot and Codex desktop clients, the default memory profile, and a link back to the source revision in Praxis Platform. If an installer is not yet validated, do not publish it as a supported release.

The release notes must distinguish local Codex/ChatGPT desktop MCP support from ChatGPT web or Work. The latter requires a separately deployed remote HTTPS/OAuth plugin and must never be represented as access to a user's local broker.
