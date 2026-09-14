# Google Tag Manager MCP Server by Insightful Pipe

[![MCP Compatible](https://img.shields.io/badge/MCP-Compatible-blue)](https://insightfulpipe.com/mcp-servers/google-tag-manager)
[![Insightful Pipe](https://img.shields.io/badge/Insightful_Pipe-MCP_Servers-purple)](https://insightfulpipe.com/mcp-servers)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> **Connect Google Tag Manager to AI assistants: audit and manage tags, triggers, variables and workspaces.**

Part of the [Insightful Pipe MCP Server Collection](https://insightfulpipe.com/mcp-servers) — use Google Tag Manager from Claude, ChatGPT, Cursor, and other AI assistants through the Model Context Protocol (MCP).

<img src="images/google-tag-manager-icon.svg" alt="Google Tag Manager MCP Server" width="64" height="64">

## MCP Server URL

```
https://google-tag-manager.insightfulmcp.com/
```

## What is Google Tag Manager MCP?

Google Tag Manager MCP is a **remote Model Context Protocol server** hosted by InsightfulPipe. Audit and manage GTM containers: tags, triggers, variables, workspaces, and versions.

## Installation

### Claude

1. Copy the MCP Server URL: `https://google-tag-manager.insightfulmcp.com/`
2. Open [Claude Connectors Settings](https://claude.ai/settings/connectors)
3. Scroll to the bottom and click **Add custom connector**
4. Paste the URL and click **Add**
5. Click **Connect** on the connector to start authorization
6. Click **Authorize access** in the browser to complete the connection

### ChatGPT

Custom MCP servers are added through ChatGPT's **Developer mode**. Availability depends on your ChatGPT plan, and workspace admins may need to allow it.

1. Turn on **Developer mode** in ChatGPT settings
2. Create a new app for a remote MCP server and paste the URL: `https://google-tag-manager.insightfulmcp.com/`
3. Authorize with your InsightfulPipe account

See OpenAI's guide: [Developer mode and MCP apps in ChatGPT](https://help.openai.com/en/articles/12584461-developer-mode-and-mcp-apps-in-chatgpt)

### Claude Code

```bash
claude mcp add --transport http google-tag-manager https://google-tag-manager.insightfulmcp.com/
```

### Cursor

Add the server to `~/.cursor/mcp.json` (all projects) or `.cursor/mcp.json` (one project):

```json
{
  "mcpServers": {
    "google-tag-manager": {
      "url": "https://google-tag-manager.insightfulmcp.com/"
    }
  }
}
```

Then authorize the connection when Cursor prompts you.

## Available Actions

61 actions: 38 read, 23 write.

### Read Actions (38)

<details>
<summary>Show all 38 read actions</summary>

| Action | Description |
|--------|-------------|
| `get_account` | Fetch a single GTM account by id |
| `get_accounts` | List all GTM accounts the authenticated user can access |
| `get_built_in_variables` | List built-in variables enabled in the workspace |
| `get_client` | Fetch a single server-side client |
| `get_clients` | List server-side clients in a workspace |
| `get_container` | Fetch a single container by id |
| `get_container_snippet` | Get the install <script> snippet for a container |
| `get_containers` | List containers in a GTM account |
| `get_destination` | Fetch a single destination |
| `get_destinations` | List destinations linked to a container |
| `get_environment` | Fetch a single environment |
| `get_environments` | List environments configured for a container |
| `get_folder` | Fetch a single folder |
| `get_folder_entities` | Return tags / triggers / variables that live inside a folder |
| `get_folders` | List folders in a workspace |
| `get_gtag_config` | Fetch a single Google Tag config |
| `get_gtag_configs` | List Google Tag (gtag.js) configurations in a workspace |
| `get_latest_version_header` | Fetch the most recent version header |
| `get_live_version` | Fetch the version currently published to live |
| `get_tag` | Fetch a single tag |
| `get_tags` | List all tags in a workspace |
| `get_template` | Fetch a single custom template |
| `get_templates` | List custom templates in a workspace |
| `get_transformation` | Fetch a single transformation |
| `get_transformations` | List server-side transformations in a workspace |
| `get_trigger` | Fetch a single trigger |
| `get_triggers` | List all triggers in a workspace |
| `get_variable` | Fetch a single variable |
| `get_variables` | List user-defined variables in a workspace |
| `get_version` | Fetch a single container version including all entities at that point in time |
| `get_version_headers` | List lightweight version headers (id, name, entity counts) without full entity payloads |
| `get_workspace` | Fetch a single workspace |
| `get_workspace_status` | Show pending changes in a workspace and any merge conflicts vs the latest container version |
| `get_workspaces` | List workspaces (staging areas) in a container |
| `get_zone` | Fetch a single zone |
| `get_zones` | List zones in a workspace |
| `lookup_container` | Look up a container by its public id (e.g. GTM-XXXXXX) |
| `quick_preview_workspace` | Generate a debug-mode preview of a workspace without saving it as a version |

</details>

### Write Actions (23)

| Action | Description |
|--------|-------------|
| `create_folder` | Create a folder for organizing workspace entities |
| `create_tag` | Create a tag in a workspace |
| `create_trigger` | Create a trigger in a workspace |
| `create_variable` | Create a variable |
| `create_workspace` | Create a new workspace (staging area) |
| `delete_folder` | Delete a folder from a workspace |
| `delete_tag` | Delete a tag from a workspace |
| `delete_trigger` | Delete a trigger from a workspace |
| `delete_variable` | Delete a user-defined variable from a workspace |
| `delete_workspace` | Delete a workspace |
| `disable_built_in_variable` | Disable one or more built-in variables in a workspace |
| `enable_built_in_variable` | Enable one or more built-in variables in the workspace by passing their type names as a comma-separated query value or repeated 'type' params |
| `move_entities_to_folder` | Move tags / triggers / variables into a folder |
| `resolve_conflict` | Resolve a merge conflict surfaced by sync_workspace by picking which side wins for a given entity |
| `revert_folder` | Discard a folder's uncommitted workspace changes |
| `revert_tag` | Discard a tag's uncommitted workspace changes, reverting it to the live container state |
| `revert_trigger` | Discard a trigger's uncommitted workspace changes |
| `revert_variable` | Discard a variable's uncommitted workspace changes |
| `sync_workspace` | Pull the latest container changes into a workspace, surfacing conflicts that need manual resolution |
| `update_folder` | Update a folder |
| `update_tag` | Update a tag |
| `update_trigger` | Update a trigger |
| `update_variable` | Update a variable |

## Control What Your AI Can Do

You decide what AI agents can do with each connected account:

- **Turn individual actions on or off** for every connected account, so agents only see the actions you allow.
- **Connect as Read-only or Read & Write.** A read-only connection can only enable read actions.
- **Destructive actions stay off by default.** Actions such as deletes are disabled until an admin enables them.
- **Team access per account.** Restricted team members only use the accounts they are granted, with the read actions enabled on them.

## Usage Examples

```
"List all tags in my container's default workspace"
```

```
"Which triggers are not used by any tag?"
```

```
"Create a GA4 event tag for form submissions"
```

## Pricing

The Google Tag Manager MCP server is included in every InsightfulPipe plan, together with all other MCP servers and the CLI. Plans start at $29.99/month with a 7-day free trial. See [insightfulpipe.com/pricing](https://insightfulpipe.com/pricing) for current plans.

## Ready-Made Skills and Prompts

- [Claude skills for measurement and analytics](https://insightfulpipe.com/marketing-claude-skills/measurement) — ready-made skills that run on your connected data

## Explore More MCP Servers by Insightful Pipe

Visit **[insightfulpipe.com/mcp-servers](https://insightfulpipe.com/mcp-servers)** to discover our full collection of MCP servers.

- [Google Analytics MCP](https://insightfulpipe.com/mcp-servers/google-analytics)
- [Microsoft Clarity MCP](https://insightfulpipe.com/mcp-servers/clarity)

**[View All MCP Servers →](https://insightfulpipe.com/mcp-servers)**

## Resources

- [Documentation](https://insightfulpipe.com/docs)
- [Video Tutorial](https://www.youtube.com/playlist?list=PLJNzvjxzI5Xwe__BJJLAelSF0ewO3mEFk)
- [InsightfulPipe Blog](https://insightfulpipe.com/blog)

## Support

- **Documentation**: [insightfulpipe.com/docs](https://insightfulpipe.com/docs)
- **All MCP Servers**: [insightfulpipe.com/mcp-servers](https://insightfulpipe.com/mcp-servers)
- **Email**: support@insightfulpipe.com

---

**[Insightful Pipe](https://insightfulpipe.com)** — AI-powered marketing analytics through MCP servers. [Explore all integrations →](https://insightfulpipe.com/mcp-servers)

## License

MIT License - see [LICENSE](LICENSE) for details.
