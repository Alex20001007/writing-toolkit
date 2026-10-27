---
name: x-crypto-tech-copy
description: 每 30 分鐘為 X 產出 10 則繁體中文加密/AI/科技/宏觀文案，素材改讀 Apify 抓回的 tweets_*.json（不再用 WebSearch）。
---

你的任務：為 X (Twitter) 產出 **10 則**可直接發佈的繁體中文貼文草稿，依當天 X 實際熱點動態分群。

# ⚙️ 引擎：讀 Apify JSON（不再用 WebSearch / 不連 Apify live）
素材來源 = 外部機器用 Apify 抓好、同步進來的 `tweets_*.json`。
本任務只負責「讀檔 → 24h 過濾 → 分層 → 寫文案」。真實 views/likes/RT 用 JSON 內的數字（無則標 `~`）。

# 🚫🚫 排除來源（全路徑 reject）
在這裡列出不想引用的網域：`{{EXCLUDED_DOMAINS}}`（例：`example-a.com`、`example-b.com`）。JSON 內若混入這些網域的轉述，跳過。

# ⚠️ 鐵律：滾動 24 小時內
```bash
NOW_EPOCH=$(date +%s); CUTOFF_EPOCH=$((NOW_EPOCH - 86400))
```
每則貼文的來源 `createdAt` 必須 ≥ CUTOFF。看不到 24h 證據 → reject，禁止用「事件還在發酵」放舊。

# ⚠️ URL 規則
每則必須具體 `https://x.com/handle/status/ID`（❌ 主頁）。JSON 內 `url` 欄已是具體 status；缺 ID → reject。

# ⚠️ 每則必附三件套
🔗 來源 URL · 💬 原文摘錄 ≤ 60 字加引號（取自 `text`）· 📊 流量訊號（`views`/`likes`/`retweets`，無則標 proxy `~`）

---

# Step 0 — 時間守門
```bash
echo "現在台北：$(TZ='Asia/Taipei' date '+%Y-%m-%d %H:%M:%S')"
H=$(TZ='Asia/Taipei' date +%H); M=$(TZ='Asia/Taipei' date +%M)
if [ "$H" -lt 9 ]; then echo "⏰ 早於 09:00。"; exit 0; fi
if [ "$H" -gt 18 ] || { [ "$H" = "18" ] && [ "$M" -gt 5 ]; }; then echo "⏰ 晚於 18:00。"; exit 0; fi
echo "✅ 守門通過。"
```

# Step 1 — 日期 + 對齊時間
```bash
TODAY=$(TZ='Asia/Taipei' date +%Y-%m-%d)
TODAY_SHORT=$(TZ='Asia/Taipei' date '+%b %d')
WEEKDAY=$(TZ='Asia/Taipei' date '+%A')
NOW_EPOCH=$(date +%s); CUTOFF_EPOCH=$((NOW_EPOCH - 86400))
H=$(TZ='Asia/Taipei' date +%H); M=$(TZ='Asia/Taipei' date +%M)
if [ "$M" -lt 15 ]; then ALIGNED="${H}:00"
elif [ "$M" -lt 45 ]; then ALIGNED="${H}:30"
else NEXT_H=$((10#$H + 1)); ALIGNED=$(printf "%02d:00" $NEXT_H); fi
```

# Step 2 — 找最新的 tweets JSON
在已連接的資料夾找最新一個 `tweets_*.json`（用 Glob / ls）。
```bash
LATEST=$(ls -t <連進來的資料夾>/tweets_*.json 2>/dev/null | head -1)
echo "使用素材：$LATEST"
```
- 找不到任何檔 → 輸出「素材缺：外部 Apify 尚未產出 JSON」報告並 exit（禁止改用 WebSearch 補）。
- 最新檔的最新 `createdAt` 距現在 > 90 分鐘 → 在輸出標註「素材偏舊，外部抓取可能停擺」，仍只用 24h 內的項目。

# Step 3 — 載入 + 24h 過濾 + 去黑名單
讀 JSON，把每則的 `createdAt` 轉 epoch，只留 `≥ CUTOFF_EPOCH`。
丟掉：`url` 不含 `/status/` 的、文字含排除網域轉述的、純轉推無觀點的。
依 `likes + retweets + views/100` 粗排出高流量候選。

# Step 4 — 分層挑選（目標 1 / 2 / 6 / 1）
- 🟩 **Layer B（2 則）**：handle ∈ {WuBlockchain, BullTheoryio} 各挑 1（不足見例外）。
- 🟥 **Layer C（6 則）**：其餘 KOL，**中文 handle ≥ 2**（sanyi_eth_/evilcos/EmberCN/ai_9684xtpa/PhyrexNi/lanhubiji/cnLedger/KuiGas… 等），其餘補英文；同 ticker ≤ 3 且角度不同。
- 🟦 **Layer A（1 則）**：純新聞事件型（快訊帳號 DeItaone/WatcherGuru/tier10k/Techmeme 等），跟 C 不重複。
- 🟧 **Layer D（1 則）**：JSON 內若含 Reddit/HN 來源項則用；無則見例外。

# Step 5 — 動態分群
自然歸納 ≥ 3 主題群（emoji + 短標籤），同群最多 3 則。

# Step 6 — 寫文案
Hook（爭議/反差/數字+反差/提問）；繁中 + ticker 英文；≤ 280 字元；1–3 hashtag；嚴禁逐字搬運原文；每則帶立場/洞察。

# Step 7 — 不足 10 則
只能在「24h 內、具體 status」前提下調整層級配比，**禁止放舊內容湊數**。補不滿 → 接受 7–9 則 + 備註。

# Step 8 — 輸出格式（直接顯示本文）
```
# 🪙 X 文案 10 則 — {TODAY} {ALIGNED}（{WEEKDAY}）

> 本輪主題群：{標籤1} / {標籤2} / {標籤3}
> 時效範圍：{CUTOFF 台北} ~ 現在（24h rolling）
> 素材檔：tweets_xxxx.json（最新項 {N} 分鐘前）
> 排除來源：{{EXCLUDED_DOMAINS}} ✅

## 1️⃣ {動態標籤} 標題（帶觀點） 🟦
> 文案本體（含 hashtag）
🔗 [@handle](https://x.com/handle/status/ID) · {N}h ago
💬 「<原文 ≤ 60 字>」
📊 {views} views / {likes} likes / {rt} RT（或 ~proxy）

## 2️⃣–3️⃣ 🟩 (WuBlockchain / BullTheoryio)
## 4️⃣–9️⃣ 🟥 (中文 ≥ 2 + 英文)
## 🔟 🟧 (Reddit/HN，若有)

---
### 🧭 本輪自查
時效範圍 / 黑名單 0 / Layer 1/2/6/1 / 主題群數 / 中文 KOL 數 / URL 全具體 / 素材檔時間 / 最新~最舊
```

# 自查表
1. ✅ 10 對 10（或備註）
2. ✅ 所有來源 createdAt ≥ CUTOFF（24h 內）
3. ✅ 0 個含排除網域
4. ✅ 跨 ≥ 3 主題群
5. ✅ 0 純報價
6. ✅ 同 ticker ≤ 3
7. ✅ 中文 KOL ≥ 2
8. ✅ 每則含 URL + 摘錄 + 流量訊號
9. ✅ Layer 分布 1/2/6/1
10. ✅ URL 全具體 status

# 例外處理
- 找不到 JSON 或全部過 24h → 輸出「素材缺/過舊」報告，exit，**不 fallback WebSearch**。
- Layer B 當日無新貼 → 1/0/8/1 備註。
- Layer D 無社群來源 → 1/2/7/0 備註。
- 中文 KOL 不足 2 → 至少 1 + 備註。

🚫 絕對禁止：超過 24h、主頁 URL 充當 status、引用排除網域、用「事件還在發酵」放舊、為湊數放舊內容、回頭用 WebSearch。
