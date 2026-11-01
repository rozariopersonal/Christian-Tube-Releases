# Bible Vocabulary Builder Progress (Normalized 2-Table Architecture)

* **Status:** `RUNNING (3 parallel chapter workers)` 🟢
* **Last Updated:** `Sunday, Nov 01, 2026 at 08:31:11 PM IST` *(Refreshed every 5s)*
* **Current Location:** Book `42:22:35` — **Luke (லூக்கா)**
* **Activity:** `LLM Single-Pass (4 new, 0 amb)`
* **Inference Engine:** `llama-server (Intel Arc Vulkan0)` (20.2ms)
* **Completed Chapters:** `994 / 1189` (83.6%)
* **Unique Surface Words in DB:** `79,815 / 95,634` (83.46%)
* **Unique Base Lemmas:** `19,508`
* **Verse Tokens Covered:** `356,693 / 418,550 words` (85.2%)
* **Compounding Cache Hit Rate:** `85.5%` (3,496 0ms hits / 591 LLM definitions)
* **Outputs Live:** SQLite (`taobvsi_glossary.sqlite` — `79,815` unique words, `356,693` verse tokens), CSV (`taobvsi_verse_words.csv` — `96.96 MB`)
* **Elapsed Time:** `1 hr, 38 mins` | **Estimated ETA (Unique Word Model):** `~1 day, 19 hrs, 48 mins (Est. Completion: Tuesday, Nov 03, 2026 at 04:19 PM IST)`

### ⚡ Worker Status

| Attribute | Current Value |
| :--- | :--- |
| **Current Book & Chapter** | Book `42:22:35` (Luke (லூக்கா)) |
| **Current Task** | `LLM Single-Pass (4 new, 0 amb)` |
| **Unique Words in Database** | `79,815` unique surface words |
| **Unique Base Lemmas** | `19,508` dictionary roots |
| **Session Words Parsed** | `4,056` |
| **Session DB Cache Hits** | `3,496` (0ms instant resolution) |
| **Session LLM Definitions** | `591` |
| **Last Verse Duration** | `57s (57.5s)` |

### 🏥 Model & Engine Health

| Metric | Current Value | Status |
| :--- | :--- | :--- |
| **Active Inference Server** | `llama-server (Intel Arc Vulkan0)` (@ `http://127.0.0.1:8080`) | 🟢 Healthy |
| **Ping Latency** | `20.2 ms` | 🟢 Active |
| **Model** | `gemma4:12b` | 🟢 Loaded |
| **Normalized Storage** | `unique_words` (~95k target) + `verse_tokens` (418,550 target) | 📚 Zero Contamination |
| **Consecutive Errors** | `0` | 🟢 0 |
