# Release publishing

This repository is a release distribution and support surface. It does not build release artifacts.

## Source of truth

The Scout adapter, its tests, and release-generation workflow live in the Praxis Platform monorepo. A public release is published here only after that workflow has produced a versioned artifact and retained its verification evidence.

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
