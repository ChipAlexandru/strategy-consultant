# Connectors

## How tool references work

Plugin files use `~~category` as a placeholder for whatever tool the user connects in that category. For example, `~~document storage` might mean Google Drive, SharePoint, or any other document platform with an MCP server.

Plugins are **tool-agnostic** — they describe workflows in terms of categories rather than specific products. The `.mcp.json` pre-configures specific MCP servers, but any MCP server in that category works.

## Connectors for this plugin

| Category | Placeholder | Included servers | Other options |
|----------|-------------|-----------------|---------------|
| Document storage | `~~document storage` | Google Drive\*, Microsoft 365 (SharePoint/OneDrive) | Box, Dropbox, Egnyte |

\* Placeholder — MCP URL not yet configured

## Notes

This plugin works fully without any connectors — all core functionality uses built-in web search, file creation, and document generation capabilities. The document storage connector is an optional enhancement for teams that want to:

- **Pull client briefs** directly from a shared drive during problem definition
- **Save final reports** to a shared drive after delivery
- **Access reference materials** stored in team document repositories
