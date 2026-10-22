# Work remotely with CodeRook

This workflow is available to every CodeRook account. The connector acts as the person who connected it and obeys that person's project permissions and the project's AI settings. Installing a plugin does not copy another user's projects, drafts, recipes, task notes or credentials.

## Open and resume

Ask your assistant to list your CodeRook projects, then open a workspace from the intended saved version and Track. Choose any meaningful workspace name. Another device or assistant signed in as the same user can resume the same workspace ID; another user opens their own private draft.

Use the workspace tools to read/search source, make explicit edits and review the diff. The assistant's ordinary local terminal and filesystem tools operate on its local folder. They do not modify or test the remote draft.

Keep the workspace revision and original file hashes with each edit. A lost response can be retried with the same operation key and arguments. A revision conflict requires reading the current state and reconciling the changes. Follow pagination and omission markers before claiming a complete search or review.

Saving uses CodeRook's normal complete-version, Track and merge rules. It reuses unchanged stored files rather than making an incomplete version from a downloaded subset. Saving, releasing and deploying are separate actions.

## Configure project jobs

A project administrator creates a manual workflow in the project's Actions screen, choosing its command, working directory, execution platform, timeout and artifact paths. Its ID is available from the authenticated project workflows API, `GET /v1/repositories/{project-id}/workflows`.

Bind that workflow to a named workspace recipe using CLI 0.38.0 or later:

```text
cbx workspace recipe my-project check --data-file recipe.json
```

Example `recipe.json`, with the project's actual workflow ID substituted:

```json
{
  "workflowId": "COPY_THE_PROJECT_WORKFLOW_ID_HERE",
  "kind": "check",
  "includePaths": ["web"],
  "secretNames": []
}
```

`kind` can be `check`, `build`, `preview` or `deploy`. An empty `includePaths` selects the full saved tree; otherwise only those file/folder prefixes are materialised on the executor. Include shared source and lockfiles needed by the command. Each job freezes its draft revision, source digest and recipe command/configuration. The assistant can inspect the configured command through `workspace_info` before queuing it.

Hosted jobs use CodeRook's available hosted capacity and account limits. They are picked up by the scheduled runner, so a queued job may wait until the next minute tick. The user's desktop can be off. Test/build/preview jobs receive no project credentials.

For native jobs, set the workflow's platform/labels and the recipe's `runnerName`, then start the matching `cbx runner` on a compatible connected machine. The CLI downloads only the selected frozen inputs to its temporary job folder. Native code runs as the user of that machine; configure it for projects you trust. Hardware, toolchains, local models and local services need to exist on that executor.

## Configure deployment

A deployment recipe names its exact target, credential names in the project's secret store, and any required check/build recipes:

```json
{
  "workflowId": "COPY_THE_DEPLOYMENT_WORKFLOW_ID_HERE",
  "kind": "deploy",
  "target": "staging",
  "secretNames": ["DEPLOY_TOKEN"],
  "requiredRecipes": ["check"]
}
```

Use the project's established deployment command. Deploy only an explicitly requested saved version whose content matches the reviewed workspace, with the current required checks passing. Only configured credential names are supplied. Inspect the job and hosting provider's result before claiming the application is live. An uncertain deployment outcome is not automatically retried.

Interactive previews need a project-specific hosting recipe/output. This connector does not supply a universal private preview gateway or turn a Linux hosted runner into a Windows desktop session.

## Permissions and handover

Reconnect an existing OAuth connection to approve the new workspace scopes. Reading uses normal project read access; editing needs `workspaces:write`, execution needs `workspaces:run`, and deployment additionally needs `workspaces:deploy` and project administration rights. Recipe configuration needs project write and workspace execution grants, plus project administration rights.

For CLI/native access, create an appropriately scoped token in CodeRook's account settings. The token form offers workspace grants explicitly and can limit a token to the selected project. Keep its value out of source and chat. The original `cbx mcp` stays read-only; `cbx mcp --workspaces` opts into the remote workflow.

Use the workspace handover note for the task, decisions, last checks and next step. It shares project state across devices; it does not transfer proprietary assistant chat history or signed-in accounts.
