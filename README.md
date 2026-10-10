# CodeRook for Claude

Work with your [CodeRook](https://coderook.com) projects from Claude. CodeRook is a version host
where every version is a complete snapshot of a project: restoring one never depends on the versions
around it, undoing deletes nothing, and taking a version down removes its files while the history
keeps a record that it existed.

This plugin gives Claude the CodeRook connector and a skill that explains how to use it well.

## What Claude can do with it

**Read** (runs without asking):

- list your projects, and the versions of a project, newest first
- list the files in a version, and read a text file at any version
- compare two versions to see which files were added, changed or removed
- search the projects people have made public

**Manage** (Claude asks you before every one of these):

- name a version, add notes, or release it
- hide a version from people outside the project, or show it again
- undo a project to an earlier version — nothing is deleted or renumbered
- take down a version's files, for something published by mistake (needs a second, explicit yes)
- change who can see a project: private, unlisted or public (opening it up needs a second yes)

A project whose owner has set it so machines may not read it stays closed to the connector.

## Setting it up

Install the plugin, then connect CodeRook when Claude asks. You are sent to coderook.com to sign in
and approve the connection; the page lists exactly what Claude will be able to do. The connection
appears among your access tokens on coderook.com, where you can end it at any time.

Saving new versions still happens on your computer, with the CodeRook desktop app, the `cbx` command
line, or `git push` to a CodeRook remote. Documentation: <https://coderook.com/docs#connector>.

## What this plugin runs and sends

- It runs no code on your machine. It contains one skill (instructions for Claude) and one remote
  MCP server entry.
- The MCP server is CodeRook's own, at `https://api.coderook.com/mcp`. Claude sends it the tool
  calls you ask for — for example a project name and a file path — over HTTPS, with the token you
  approved. Nothing is sent anywhere else.
- CodeRook does not receive your conversation with Claude, only the tool calls themselves. How
  CodeRook handles account data is in its [privacy policy](https://coderook.com/privacy).

## Support

Email support@coderook.com. Security reports go to security@coderook.com.

CodeRook is made by ACCA Gaming Productions. Licensed under the Apache License 2.0.
