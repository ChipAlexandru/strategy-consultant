# Connectors

## How tool references work

Plugin files use `~~category` as a placeholder for whatever tool the user connects in that category. Plugins are tool-agnostic — they describe workflows in terms of categories rather than specific products.

## Connectors for this plugin

| Category          | Placeholder            | Options                                        |
| ----------------- | ---------------------- | ---------------------------------------------- |
| Document storage  | `~~document storage`   | Google Drive, Box, SharePoint, Dropbox          |
| Data/BI platform  | `~~data platform`      | Tableau, Power BI, Looker, Mode                 |
| Project tracker   | `~~project tracker`    | Asana, Linear, Jira, Monday                     |
| Chat              | `~~chat`               | Slack, Microsoft Teams, Discord                 |

## Notes

This plugin works fully without any connectors — all core functionality uses built-in web search, file creation, and document generation capabilities. Connectors are optional enhancements for teams that want to:

- **Document storage**: Save final reports directly to a shared drive
- **Data/BI platform**: Pull client dashboards or data visualizations into the analysis
- **Project tracker**: Create follow-up tasks from report recommendations
- **Chat**: Share findings or report links with team channels
