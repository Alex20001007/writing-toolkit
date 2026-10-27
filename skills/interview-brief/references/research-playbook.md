# Research Playbook

How to turn a name into a rich brief in 8-15 minutes. Work in parallel, prioritize primary sources, and log everything so the Appendix can cite it.

## Order of operations

1. **Check user's Notion first** (`notion-search`). Search the subject's name and any company aliases. If the user already has notes, start from those — don't duplicate, just extend.
2. **Fan out WebSearch queries** (run in parallel in one turn):
   - `"{name}" "{current company}"` — grounds current role
   - `"{name}" interview OR podcast OR 專訪` — finds media footprint
   - `"{name}" founded OR CEO OR CTO OR "co-founder"` — prior ventures
   - `"{name}" LinkedIn` — public profile summary (even if LinkedIn itself is gated, results often surface a cached snippet)
   - `"{name}" controversy OR lawsuit OR resigned OR stepped down` — landmines
   - `"{name}" Twitter OR X.com OR 方格子 OR Substack` — their own voice
   - If Chinese-speaking subject: add 繁中 queries with Chinese name variants
3. **Fetch the best 4-8 sources** with WebFetch. Prioritize in this order:
   - Their own posts / newsletter / personal blog
   - Full-length podcast transcripts (not summaries)
   - Company announcement posts where they're quoted at length
   - Long-form profile pieces (The Information, Bloomberg, 數位時代, 天下, 商周 long reads)
   - News items about pivots, funding, departures, legal events
4. **Gated sources**: if a LinkedIn full profile, paywalled piece, or members-only Substack looks high-value, use Claude in Chrome to fetch. Don't bother with Chrome for merely-convenient sources.
5. **Stop when you have enough.** The signal is: you can fill every section of the brief without saying "待查" more than twice. Don't keep searching for its own sake.

## What to extract from each source

Read with these prompts in mind:

- **Timeline events**: "In {year} they did X" — builds the bio
- **Quotes they repeat**: if the same phrase shows up in 2+ interviews, that's a signature talking point. Flag it. This tells you what NOT to re-ask, and what their canned narrative sounds like.
- **Quotes that seem off-message**: something they said once that doesn't fit their usual brand — highest-value material, often the thread to pull on camera.
- **Topics they redirect away from**: when an interviewer goes somewhere and the guest pivots, note both the topic and the pivot destination.
- **People they mention**: co-founders, mentors, investors, parents, spouses. The *Emotional Map* is built from these mentions.
- **Numbers**: funding amounts, team sizes, user counts, revenue. Useful for All-in-style debate questions.
- **Contradictions with prior statements**: if their 2022 interview and 2024 interview disagree on something, that's a question.

## Source quality heuristics

- **Primary (gold)**: their own words, full transcripts, their own posts
- **Secondary (silver)**: reporter profile pieces where they were interviewed
- **Tertiary (bronze)**: aggregated listicles, "top 30 under 30", promotional company bios — useful for factchecks but don't quote from them
- **Do not use**: AI-generated summary sites, content farms, outdated Wikipedia stubs as sole source for recent claims

If you only have tertiary sources for a claim, mark it `[待查]` in the brief rather than stating it as fact.

## Chinese-context specifics

For Taiwan / HK / mainland China-connected subjects:

- Search both 繁中 and 簡中 spellings
- 數位時代, 科技報橘 (TechOrange), INSIDE, 商周, 天下 — top Taiwan tech media
- 36Kr, 虎嗅, 晚點 LatePost — top mainland tech media
- 方格子 (vocus), Matters — Chinese-language personal writing platforms
- For crypto/Web3 subjects: Foresight News, PANews, Rhythm 律動, BlockTempo 動區動趨, 鏈新聞 — all have Chinese-language long-form
- Twitter/X is often the richest voice source for crypto founders — check their own timeline
- Use Claude in Chrome for logged-in LinkedIn, since LinkedIn is often the only place to see their full employment history for non-US subjects

## Landmine detection

Actively look for:
- Lawsuits (civil and criminal)
- Public feuds on social media
- Startups that failed or pivoted controversially
- Accusations of misconduct (professional or personal)
- Recent bereavements or divorces (public knowledge only)
- Health issues they've disclosed
- Political statements that aged poorly

Put these in the *Known Landmines* section. The user decides whether to go near them; your job is to make sure they don't walk in blind.

## What counts as a "less-discussed" topic

For the *少被問到的面向* section, look for:
- Specific topics the subject *has* mentioned but only once or twice, in passing
- Mentions of family members by name (almost always under-explored)
- Early-career jobs they've mostly scrubbed from their LinkedIn summary
- Hobbies (martial arts, music, religion, gaming, cooking — any of these can open someone up)
- The person they credit when they're being honest — the *real* role model, not the public one
- What they were doing the year before their first public success — the "dark year" is often unexplored territory
- Their relationship with money — most high-profile people are evasive about this, which means the question is fresh

If you can't find any such angles, say so and recommend the user probe these areas live.
