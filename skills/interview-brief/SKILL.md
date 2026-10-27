---
name: interview-brief
description: Prepare a deep pre-interview brief for a specific named person before a podcast/media/video interview. Trigger on 專訪, 訪談, 訪談稿, 受訪者, 準備訪問 X, 我要訪 OO, 幫我找 XX 的資料, 我下週要訪談, interview prep, podcast guest research, or any variant signalling the user needs background before sitting down with someone. This is the DEFAULT deliverable for interview prep — trigger even on casual mentions, even without the words brief or 稿. Produces a 中英混用 brief covering career timeline, superpowers & creations, current role and projects, media footprint (past interviews, repeated talking points, what they dodge), emotional touchpoints (family, role models, turning points, low points, under-explored topics), humor tolerance, known landmines, and a JRE / All-in Podcast-style question bank with branched follow-ups. Default output is a Notion page plus a local markdown backup.
---

# Interview Brief (深度專訪準備稿)

Generate a pre-interview brief the user can skim right before walking into an interview. The goal is for the user to feel like they already *know* the guest — their public persona, their private soft spots, what they've said a thousand times, and what's never been asked.

The user runs interviews in a style similar to **Joe Rogan Experience (PowerfulJRE)** and **All-in Podcast** — curious, willing to push back, unafraid to go personal, comfortable with humor. Questions should reflect that posture, not the polite-journalist or PR-sanitized style.

Output language is **中英混用**: narrative and section headers in 繁體中文; preserve English names, company names, quotes, and source titles in their original English.

## Inputs to gather from the user before researching

Ask concisely (one AskUserQuestion turn) for any missing pieces:
1. **Subject**: full name + current company/role (required)
2. **Interview context**: live podcast / recorded video / written / other; length; expected audience
3. **Language of the actual interview**: 中/英/雙語 — affects how phrasing examples are written
4. **Angle the user is leaning toward**, if any (e.g. "想聊他退出 Coinbase 之後的心境轉變")
5. **Any prior material the user already has** (Notion notes, prior meetings) — search user's Notion before asking them to dig it up

Skip the question if the user already supplied the info in the current conversation.

## Research workflow

See `references/research-playbook.md` for the full source checklist and fallback order. In short:
- Run WebSearch queries in parallel for biography, current work, controversies, and past interviews
- Fetch the most promising 4-8 sources with WebFetch — prefer primary sources (the person's own posts, podcast transcripts, company announcements) over tertiary recaps
- If a source is gated (LinkedIn full profile, paywalled media, Substack members-only) and worth the effort, fall back to Claude in Chrome
- Search the user's Notion with `notion-search` for any existing notes on this person — do this early, before external research, so you don't duplicate work the user has already done
- Timebox research: 8-15 minutes of parallel fetches is usually enough. Don't spiral.

Record every source you actually use so the Appendix can cite them.

## Brief structure (this is the contract)

Use the template in `assets/brief-template.md` verbatim as the scaffolding. Every section below must appear in the output, even if briefly, because the user's workflow depends on the same structure every time.

The structure maps directly to the user's five stated needs:

1. **受訪者檔案** — past experiences, strengths, creations → sections *At-a-glance bio*, *超能力與代表作*
2. **現況與媒體足跡** — current work + past interviews and what was discussed → sections *現在在做什麼*, *媒體足跡 Media Footprint*
3. **公司、職位、任務** — folded into *現在在做什麼*
4. **情感切入點** — family, friends, role models, rarely-discussed topics → sections *情感地圖 Emotional Map*, *少被問到的面向*
5. **幽默感與開得起玩笑的程度** → section *幽默 & 互動風格 Humor Profile*

Plus the interview-design payload: *已知地雷*, *建議敘事角度*, *問題庫 Question Bank*, *現場追問小抄 Live Cue Cards*, *Appendix Sources*.

See `references/question-style-guide.md` for how to design the question bank in JRE + All-in style. Do not skip this reference — the question bank is what the user actually uses on camera, and "polite journalist" style is a failure mode.

## Output: Notion page + local backup

Default delivery:
1. **Notion page** — create under the user's workspace. If the user has a dedicated "Interviews" or "專訪" database, create the page as a row there. Otherwise create a standalone page under the user's private home. See `references/notion-structure.md` for block-level formatting (toggles, callouts, H1/H2/H3 mapping).
2. **Local markdown backup** — save a `.md` copy to the outputs folder so the user can open it offline on-set. Name it `{受訪者名}-brief-YYYYMMDD.md`.

After creating both, share a single chat message with:
- A direct Notion link ("📄 已建立 Notion 頁面：[標題](url)")
- A computer:// link to the local .md backup
- A ≤3-bullet summary of *the most interesting angles* you discovered — not a recap of the sections, but the thing the user will want to lead with

## Failure modes to avoid

- **Generic bio dump.** If the brief reads like a Wikipedia summary, it's failed. The user already knows the public surface — they want the seams, the inconsistencies, the emotional pressure points.
- **Polite questions.** "Tell us about your journey" is banned. Every question should either (a) reference something specific the guest has said or done, or (b) force them off their standard narrative.
- **Skipping emotional map.** The user *specifically* asked for this. Don't shrink it because the public sources are thin — in that case, note what's missing and suggest angles the user might probe live.
- **Over-citing, under-synthesizing.** Don't just list "they said X in interview Y". Say what the pattern is: what they love to repeat, what they dodge, which of their claims have shifted over time.
- **Hallucinated quotes or affiliations.** If a fact isn't solidly sourced, mark it `[待查]` rather than inventing. This is the user's reputation on camera.

## When the subject is low-profile

If the person has minimal public footprint (common for early-stage founders, private-company execs, non-English-speaking figures), the brief still ships — but flag thin sections explicitly and lean harder on:
- Their company's public material (if they're a founder, the company IS the biography)
- Co-founders / investors' interviews that mention them
- Their own social posts (X, LinkedIn, 方格子, Substack)
- 人脈 inference: who they work with, where they went to school, who their mutual connections are

Note "public footprint is thin — recommend opening the interview with origin story to let them set the canvas."

## Tool loading

Only load tools when actually needed — don't eagerly instantiate:
- WebSearch + WebFetch: always
- Claude in Chrome browser tools: only if you hit a gated source worth fetching
- Notion MCP tools (`notion-search`, `notion-fetch`, `notion-create-pages`): always, used at both ends (prior-notes lookup and final page creation)
- AskUserQuestion: use once up front for missing inputs; avoid multi-round interrogation
