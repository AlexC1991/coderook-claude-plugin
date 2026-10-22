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
- check whether a project can serve its app's updates, and get the feed address to give the app

**Manage** (within the work you authorise):

- name a version, add notes, or release it
- hide a version from people outside the project, or show it again
- undo a project to an earlier version â€” nothing is deleted or renumbered
- take down a version's files, for something published by mistake (needs a second, explicit yes)
- change who can see a project: private, unlisted or public (opening it up needs a second yes)

A project whose owner has set it so machines may not read it stays closed to the connector.

## Setting it up

Install the plugin, then connect CodeRook when Claude asks. You are sent to coderook.com to sign in
and approve the connection; the page lists exactly what Claude will be able to do. You can end the
connection at any time from your account settings on coderook.com.

Remote drafts can now save complete versions through the connector. Local projects can still use the desktop app, `cbx` or Git. Documentation: <https://coderook.com/docs#connector>.

## Remote workspaces

From Claude Desktop's Code tab, open a CodeRook workspace through the connector. Read and search selected files, edit the private draft, review its diff, run configured checks, then save a complete version. The full project and its build dependencies stay off the laptop. The desktop PC can be off while hosted jobs run.

The same workspace ID, revision and task note work in Codex and Claude. This shares project state, not either app's chat history or signed-in accounts.

Install/update this plugin and reconnect CodeRook to approve `workspaces:write`, `workspaces:run` and `workspaces:deploy` alongside the project grants. The consent page explains each grant. Use `/mcp` to reconnect in Claude Code. Old grants retain their existing permissions.

Project administrators configure named check/build/deploy recipes. Ordinary checks receive no project credentials. Deployment recipes require an exact saved version and named target, and may require successful checks. Request the actual deployment explicitly. A build or save alone does not publish a website.

Windows builds and native app testing use a selected connected Windows `cbx runner` (CLI 0.38.0 or later). Only the recipe's selected input paths are fetched into its temporary job folder. That executor must be on; hosted checks don't need it. GPU workloads require suitable hardware. Interactive previews need a project-configured hosting target; the connector does not create a universal preview host.

## What this plugin runs and sends

- It runs no code on your machine. It contains one skill (instructions for Claude) and one remote
  MCP server entry.
- The MCP server is CodeRook's own, at `https://api.coderook.com/mcp`. Claude sends it the tool
  calls you ask for â€” for example a project name and a file path â€” over HTTPS, as the account you
  approved it for. Nothing is sent anywhere else.
- CodeRook does not receive your conversation with Claude, only the tool calls themselves. How
  CodeRook handles account data is in its [privacy policy](https://coderook.com/privacy).

## Support

Email support@coderook.com. Security reports go to security@coderook.com.

CodeRook is made by ACCA Gaming Productions. Licensed under the Apache License 2.0.
