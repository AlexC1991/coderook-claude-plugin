# CodeRook Codex public review

The Codex package under `plugins/coderook-codex/` contains the remote MCP
connection, generic skill, listing metadata and initial public-review cases.
These are for all CodeRook users. Every user signs into their own account;
installation does not copy reviewer fixtures or any other user's projects.

Version **0.2.2** adds the verified support, privacy and terms links, the existing
512px CodeRook PNG icon, five positive cases, three unsupported-operation cases,
release notes, all-country targeting and an account-only commerce declaration.
It preserves the existing package name, endpoint and starter prompt.

The review cases use sample projects on a dedicated synthetic account. Do not
put that account's credentials, session cookies or access tokens in this
repository or in the submission ZIP. Supply reviewer access only through the
Developer Portal's secure reviewer fields.

All five positive and three negative cases passed in native Codex Desktop
against version 0.2.2 using the dedicated synthetic reviewer account. The demo
reviewed and saved `codex-review-demo` v3 and read back its handover note.

The [recorded walkthrough](https://github.com/AlexC1991/coderook-claude-plugin/releases/download/codex-v0.2.2/coderook-codex-0.2.2-demo.mp4)
is 5:06 and includes all eight cases. It contains real interactions; idle time
between cases and the unrelated sidebar were removed. Playback, decoding and
scene frames were checked. An unauthenticated public download matched the
local video SHA-256:
`6026ecc640aea2cf1c2dbcd2dbc8c9b1e77bf2ce41b32cfadf26e4adf1338d45`.
The manifest includes that verified recording URL.

The completed ZIP is suitable for Portal upload. Domain/developer verification,
connection checks and scans against the exact saved Portal version, secure
reviewer access and publisher attestations remain Portal steps. No directory
submission or approval is claimed by this repository release.

Keep author-upload packages separate from private account source. Exclude root
`.app.json` and all non-null `apps` declarations in author uploads. Preserve
Portal-generated connection bindings when working on saved/finalized releases.
Inspect an existing submission before creating or replacing a draft.

Source availability and repository installation do not establish directory
approval. Submit the completed draft for review, then publish the approved
release through the normal portal flow.
