---
name: coderook
description: Work with projects on CodeRook, a version host where every version is a complete snapshot, through the CodeRook connector. Use when someone asks about their CodeRook projects, wants to see what is in a version, read a file, compare two versions, find public projects, or manage versions — name or release one, hide or show it, undo a project to an earlier version, take down files published by mistake, or change who can see a project.
---

# CodeRook

CodeRook keeps whole snapshots of a project. A version names every file the project had at that
moment, so restoring one never depends on the versions around it. There is no staging area and no
history to rewrite: undoing moves the project back without deleting anything, and taking a version
down removes its files but keeps a record that it existed.

This skill works through the **CodeRook connector**, which comes with this plugin (its tools are
named `list_projects`, `list_versions`, and so on). If those tools are not available, the person
needs to connect CodeRook: Claude offers it when the plugin is installed, and signing in happens on
coderook.com.

## Finding things

- Start with `list_projects` to learn the project slugs. Every other tool takes `project` as a slug.
- Versions are numbered (`42`, or `v42`). A named release can be used by its name. `latest` means
  the project's **current** version — after an undo that may not be the highest number.
- `list_versions` shows which version is current, which are named releases, which are hidden, and
  which were taken down.
- `list_files` lists one folder of a version (the top by default; pass `path` for a subfolder).
- `read_file` returns up to 256 KB of a text file. Binary files are reported, not shown.
- `compare_versions` lists the files added, changed and removed between two versions.
- `search_public_projects` searches what people have made public.

If a project's owner has set it so machines may not read it, the read tools say so. Respect that;
do not try to get at the files another way.

## Changing things

Every change below is real and visible to other people, so before calling a write tool, say in one
sentence what will change and get the person's agreement.

| They want to… | Use | Notes |
|---|---|---|
| Name a version / write notes | `name_version` | Naming a version for the first time needs admin rights. |
| Make it a release people are told about | `release_version` | Watchers are notified. |
| Hide a version from outsiders, or show it | `set_version_visibility` | `private` or `public`; showing needs admin rights. |
| Go back to an earlier version | `undo` | Nothing is deleted or renumbered. The versions passed over stay in the history. |
| Remove files published by mistake | `take_down_version` with `confirm: true` | Permanent for the files. The current version can't be taken down — `undo` first. |
| Change who can see the project | `set_project_visibility` | `private`, `unlisted` (anyone with the link) or `public`. Opening it up needs `confirm: true`. |

### Something was published by mistake

The usual order:

1. `undo` — puts the project back on the version before the mistake. The bad version is still in
   the history and, if it was a named release, still published.
2. `set_version_visibility` with `private` on the bad version — nobody outside the project can read it.
3. `take_down_version` with `confirm: true` and a short `reason` — its files are gone; the history
   keeps a record that it was there.

Be honest about what this does and does not do: anyone who downloaded the files before they were
taken down still has them. If what leaked lets someone sign in to another service, it must also be changed on that service.

## When something is refused

The tools answer with CodeRook's own message — for example that an action needs admin rights, that
the current version can't be taken down, or that a project needs a username before it can be public.
Pass the message on plainly and suggest the fix it names; do not retry the same call.

## Outside the connector

Saving new versions from a folder happens on the person's machine, with the CodeRook desktop app, the
`cbx` command line (`npm install -g @coderook/cli`, then `cbx submit`), or plain `git push` to a
CodeRook remote. The connector manages what is already on CodeRook; it does not upload files.
