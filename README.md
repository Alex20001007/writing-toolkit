# Writing Toolkit

Alex Chen（BlockTempo 動區動趨 Growth Manager）的寫作技能、prompt 範本與風格規則。內容從過去與 Claude 合作的稿件、技能與修改回饋整理而來。

## 目錄

```
writing-toolkit/
├── style-guide/
│   └── house-style.md          ← 先讀這份：標題、標點、結構、語氣的固定規則
├── skills/                     ← Claude Skills（SKILL.md 可直接安裝）
│   ├── deep-article-writer/    深度文章／專題／合作稿完整產線
│   ├── x-crypto-tech-copy/     X 批次文案（讀 Apify tweets JSON，10 則／輪）
│   └── interview-brief/        專訪前的深度受訪者準備稿
├── prompts/                    ← 沒有技能時直接複製貼上的範本
│   ├── 01-deep-article.md
│   ├── 02-sponsored-article.md
│   ├── 03-tutorial-article.md
│   ├── 04-x-long-post.md
│   ├── 05-event-promo.md
│   ├── 06-data-finance-article.md
│   ├── 07-ama-script.md
│   └── 08-business-docs.md
├── checklists/
│   ├── fact-redline.md         事實紅線：發稿前必跑
│   └── finance-compliance.md   金融／加密題材合規禁語與替代說法
└── case-notes/
    └── README.md               過去稿件的定調決策與修改紀錄（已去識別化）
```

## 怎麼用

| 要寫的東西 | 用什麼 |
| --- | --- |
| 深度文、產業分析、合作稿 | `skills/deep-article-writer` 或 `prompts/01`、`02` |
| 工具教學、開戶教學 | `prompts/03` |
| X 長文、參訪心得 | `prompts/04` |
| X 每日批次貼文 | `skills/x-crypto-tech-copy` |
| Hackathon／活動宣傳 | `prompts/05` |
| 數據回測型財經文 | `prompts/06` |
| AMA、X Space、論壇主持 | `prompts/07` |
| 專訪準備 | `skills/interview-brief` |
| 提案、內部說明、商務信 | `prompts/08` |

每次動筆前把 `style-guide/house-style.md` 一起貼給 AI，發稿前跑一次 `checklists/`。

## 安裝 Skills

- **Claude.ai**：Settings → Capabilities → Skills，上傳該資料夾（或打包成 zip）。
- **Claude Code**：把資料夾複製到 `~/.claude/skills/`。

## 維護

- 有新的修改回饋，就補進 `house-style.md` 或對應 prompt。
- 新完成的稿件在 `case-notes/README.md` 加一列：定調、修改歷程、學到的規則。
- 客戶名稱、報價、邀請碼、未公開的合作資訊不要寫進來。
