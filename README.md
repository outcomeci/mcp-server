# OutcomeCI MCP Server

Connect your AI assistant to OutcomeCI to create, validate, and manage agent-powered workflows across the tools your team uses.

This is the public connection and documentation repository for OutcomeCI's hosted Model Context Protocol (MCP) server. It contains server metadata and client configuration—not the hosted backend or a self-hosted server distribution.

## Connect

Add OutcomeCI as a remote MCP server in your client:

```text
https://api.outcomeci.com/v1/mcp
```

- **Transport:** Streamable HTTP
- **Authentication:** OAuth through your browser
- **Access:** Sign in to OutcomeCI and authorize a workspace

No local server installation or shared API key is required. Each person authorizes their own connection. Your client must support remote Streamable HTTP servers and OAuth.

### Setup guides

- [Claude](https://outcomeci.com/content/guides/claude-mcp-setup)
- [Claude Code](https://outcomeci.com/content/guides/claude-code-mcp-setup)
- [Codex](https://outcomeci.com/content/guides/codex-mcp-setup)
- [ChatGPT](https://outcomeci.com/content/guides/chatgpt-mcp-setup)

For clients that accept this configuration format, see [the example configuration](examples/claude-code.mcp.json). Other clients may use different field names; follow their remote-server setup instructions.

## Try it

Ask your connected assistant:

> List the workflows in my OutcomeCI workspace.

> Read the workflow schema and help me create a workflow that turns a Slack request into a GitHub pull request. Validate it before saving.

> Show the recent runs for my workflow and inspect the logs for the latest failure.

Available tools depend on the permissions granted to the connection. Configuring a workflow may also require connectors, credentials, and an agent connection.

## Tools

The server exposes the following tools. Your client's live `tools/list` response is authoritative for the current schemas and authorized tool set.

| Tool | What it does |
| --- | --- |
| `list_workspaces` | Show the workspace authorized for the connection. |
| `list_workflows` | List workflows and their latest metadata. |
| `get_workflow` | Read a workflow's latest definition and support files. |
| `get_workflow_schema` | Get the current `outcome.yml` contract and an example. |
| `get_connector_schema` | Inspect a connector's operations and credential requirements. |
| `get_integration_setup_guide` | Get setup guidance for an integration. |
| `validate_workflow` | Validate a complete workflow package without saving it. |
| `create_workflow` | Create a workflow and its first version. |
| `upload_workflow_version` | Save a new immutable version with checks against concurrent changes. |
| `configure_workflow_trigger` | Configure supported email or webhook triggers. |
| `create_credential_deposit` | Create a secure UI link for depositing a credential. |
| `get_credential_deposit_status` | Check a deposit's status without retrieving its secret. |
| `list_vault_entries` | Inspect credential metadata and grants, not secret values. |
| `list_agent_connections` | List connected agents' metadata. |
| `list_workflow_runs` | List recent runs for a workflow. |
| `get_workflow_run_logs` | Read paginated run logs. |
| `cancel_workflow_run` | Request cancellation of an active run. |

## Permissions and credentials

Authorize only the workspace and permissions you intend to give your assistant. Use your client's approval controls for changes such as saving workflows, configuring triggers, or cancelling runs.

Never paste credentials into chat. Use the secure deposit link when a workflow needs a secret. Treat deposit links, inbound webhook URLs, and run logs as potentially sensitive; do not include them in public issues.

## Pricing

OutcomeCI Cloud usage is billed according to [OutcomeCI pricing](https://outcomeci.com/pricing). Connecting an assistant does not make workflow execution free.

## Documentation and feedback

- [OutcomeCI](https://outcomeci.com)
- [Connect an agent](https://outcomeci.com/docs/outcomeci/connect-agent)
- [Workflow documentation](https://outcomeci.com/docs/outcomeci/workflow)
- [Vault documentation](https://outcomeci.com/docs/outcomeci/vault)

For documentation problems or feature requests, [open an issue](https://github.com/outcomeci/mcp-server/issues). Include the client name and a sanitized description; never include tokens, secrets, or private workflow data.

## Repository metadata

[server.json](server.json) describes the hosted endpoint using the MCP Registry server schema. Its version tracks this repository's metadata, not a pinned version of the hosted service. Including the manifest does not imply that a directory or registry has approved the listing.
