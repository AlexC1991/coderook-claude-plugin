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

Public directory review also needs a real, accessible walkthrough recording,
host behavior tests, domain/developer verification, required scans and publisher
attestations. Add a verified recording URL to
`extensions.com.openai.review.demo_recording_url` when the recording is ready;
do not insert a placeholder or describe a script as a completed video.

Keep author-upload packages separate from private account source. Exclude root
`.app.json` and all non-null `apps` declarations in author uploads. Preserve
Portal-generated connection bindings when working on saved/finalized releases.
Inspect an existing submission before creating or replacing a draft.

Source availability and repository installation do not establish directory
approval. Submit the completed draft for review, then publish the approved
release through the normal portal flow.
