# Support boundaries

Use GitHub issues here for end-user installation, upgrade, compatibility, and documentation problems. This keeps the public support record separate from the implementation and CI work in Praxis Platform.

## Include

- PluresLM Scout release version;
- Windows version and architecture;
- Scout or Copilot host version;
- the installation step that failed;
- redacted logs and the artifact checksum, when available.

## Do not include

- memory database files or memory contents;
- bearer tokens, API keys, or session data;
- private repositories, code, or user prompts;
- unreleased implementation details.

For a suspected vulnerability, do not open a public issue containing exploit details or secrets. Use the repository's private security-reporting path when it is available.

## Scope

The Scout adapter is a client of the shared PluresLM service. Storage ownership, service policy, and implementation changes belong in Praxis Platform. This repository carries the resulting release artifacts and user-facing documentation.
