# Notion Page Structure

How to render the markdown template into Notion blocks that read well on both desktop and mobile. The user will likely open this on their phone right before the interview.

## Placement

1. First, `notion-search` for a database/page with title containing "專訪", "Interview", "Podcast", or "訪談". If found, create the brief as a child page (or as a row in the database if it's a database).
2. If not found, create a top-level page in the user's private workspace titled: `專訪 — {{受訪者中文名}} ({{English Name}}) — {{YYYY-MM-DD}}`
3. Don't create a new database without asking. Prefer adding to existing structure.

## Block mapping

Map each markdown section in `assets/brief-template.md` to Notion blocks as follows:

| Markdown | Notion block |
|---|---|
| `# title` | `heading_1` |
| `## section` | `heading_2` |
| `### subsection` | `heading_3` |
| `> quote / callout` | `callout` (use 💡 or ⚠️ icons by context) |
| Speed-read 30-second card | `callout` with `blue_background`, icon ⚡ |
| 已知地雷 section header | `heading_2` + opening `callout` with ⚠️ icon, `red_background` |
| 幽默 & 互動風格 | `callout` summary at top with 😄, then details below |
| Question bank questions | `numbered_list_item` for main Q, `toggle` for the follow-up branches (so they can expand on phone without clutter) |
| Sources table | `table` block |
| `[待查]` items | use `code` inline, so they're visually scannable |

## Must-do formatting details

- **Cover and icon**: set an icon (emoji 🎙️ is safe default) and a cover image if a good portrait is available. A brief with no icon/cover feels unloved.
- **Properties (if the host is a database)**: 受訪者, 公司, 職位, 訪談日期, 狀態 (Preparing / Ready / Done), Humor Profile (High/Med/Low)
- **Table of contents**: add a `table_of_contents` block right after the Quick Card so the host can jump on mobile
- **Synced block trick** (optional): if the Live Cue Cards section would be useful across multiple briefs, consider making it a synced block — but default to inline for simplicity

## Delivery message to user

After creation, the user message should be short:

```
📄 Notion 頁面已建立: [專訪 — {{name}} — {{date}}]({{notion_url}})
💾 本地備份 (MD): [view](computer:///.../{{name}}-brief-{{date}}.md)

三個我建議你 lead 的角度:
• {{angle 1}}
• {{angle 2}}
• {{angle 3}}

需要我調整哪個部分？
```

Don't dump the whole brief back into chat — the user will read it in Notion.

## Fallback if Notion MCP is unavailable

If the Notion tools aren't loaded/connected, tell the user once, offer to:
1. Output only the local .md file
2. Output a copy-paste-ready block that they can dump into Notion themselves

Don't spend cycles trying to debug Notion connectivity — the brief itself is the deliverable.
