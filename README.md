# Christian Tube CDN & Open Study Datasets

High-performance, edge-cached static datasets for **Christian Tube** (Mobile & Web). All assets are chunked into lightweight, chapter-level JSON files and globally distributed via the **jsDelivr CDN** and GitHub Pages.

---

## 🌐 Global CDN Base URLs

Primary CDN (Fastly / Cloudflare Edge):
```http
https://cdn.jsdelivr.net/gh/rozariopersonal/Christian-Tube-Releases@main/
```

Fallback URL (Raw GitHub):
```http
https://raw.githubusercontent.com/rozariopersonal/Christian-Tube-Releases/main/
```

> [!NOTE]
> All endpoints return pre-formatted UTF-8 JSON with global CORS enabled (`Access-Control-Allow-Origin: *`). Every chapter or chunk is typically **1 KB – 8 KB**, compressing to **< 2 KB** with Brotli/gzip.

---

## 📁 Repository Structure

```
Christian-Tube-Releases/
├── README.md                          # Documentation and schema guide
├── index.json                         # Global manifest of all datasets
│
├── bibles/                            # Multi-version Scripture dataset
│   ├── bible_{version}.json           # Monolithic version archive for offline download
│   └── {version_id}/                  # e.g., web, kjv, taobvsi, mal_irv, hin_irv, etc.
│       ├── books.json                 # List of books, names, chapter counts
│       └── {book_number}/             # 1 (Genesis) to 66 (Revelation)
│           ├── 1.json                 # Chapter 1 verses [{ verse, text }]
│           └── {chapter}.json
│
├── books/                             # Zac Poonen & Annie Poonen Christian Library
│   ├── catalog.json                   # All 38 books metadata (title, author, subject, pages)
│   ├── books.sqlite.gz                # Full SQLite database archive for offline mobile use
│   └── {book_id}/                     # e.g., beauty_for_ashes, a_godly_family_life
│       ├── toc.json                   # Table of Contents with chapters, line/page ranges
│       └── chapters/
│           ├── 1.json                 # Lines [{ line, page, text, isHeading, headingLevel }]
│           └── {chapter_index}.json
│
├── commentaries/                      # Verse-by-verse commentary expositions
│   └── {book_number}/                 # 1 to 66
│       └── {chapter}.json             # Verses with linked book passages & headlines
│
├── cross_references/                  # Treasury of Scripture Knowledge (TSK) links
│   └── {book_number}/
│       └── {chapter}.json             # Verses mapped to cross-references
│
├── backgrounds/                       # Historical and cultural background notes
│   └── {book_code}/                   # e.g., gen, mat
│       └── {chapter}.json             # Archaeological, cultural, historical context
│
├── words_feed/                        # Micro-Feed / Daily Devotionals
│   ├── manifest.json                  # Topics manifest with item counts
│   ├── daily.json                     # 365 daily devotionals
│   └── topics/
│       └── {topic_slug}.json          # e.g., faith.json, prayer.json, love.json
│
└── dictionaries/                      # Offline dictionary SQLite archives
    └── dict_{dict_id}.sqlite.gz       # Easton's, Strong's, Tamil, Malayalam, Hindi, etc.
```

---

## 📖 API Endpoints & Schemas

### 1. Bibles (Multi-Version Scripture)

#### Books List
* **URL**: `GET /bibles/{version_id}/books.json`
* **Example**: `/bibles/web/books.json`
```json
[
  { "bookNumber": 1, "name": "Genesis", "chapters": 50 },
  { "bookNumber": 43, "name": "John", "chapters": 21 }
]
```

#### Chapter Verses
* **URL**: `GET /bibles/{version_id}/{book_number}/{chapter}.json`
* **Example**: `/bibles/web/43/14.json` (John 14 in World English Bible)
```json
[
  { "verse": 1, "text": "“Don’t let your heart be troubled. Believe in God. Believe also in me." },
  { "verse": 27, "text": "Peace I leave with you. My peace I give to you..." }
]
```

**Supported Bible Versions**:
- `web` (World English Bible)
- `kjv` (King James Version 1611)
- `asv` (American Standard Version 1901)
- `bbe` (Bible in Basic English)
- `ylt` (Young's Literal Translation)
- `taobvsi` (Tamil Old Version / Bower-Balfour)
- `mal_irv` (Malayalam Indian Revised Version)
- `tel_irv` (Telugu Indian Revised Version)
- `kan_irv` (Kannada Indian Revised Version)
- `hin_irv` (Hindi Indian Revised Version)
- `elberfelder`, `luther1545` (German)
- `martin` (French)
- `diodati`, `riveduta` (Italian)
- `sse` (Spanish)
- `statenvertaling` (Dutch)
- `polgdanska` (Polish)

---

### 2. Books Library (38 Volumes by Zac & Annie Poonen)

#### Books Catalog
* **URL**: `GET /books/catalog.json`
```json
[
  {
    "id": "beauty_for_ashes",
    "title": "Beauty for Ashes",
    "author": "Zac Poonen",
    "subject": "The Cross and Discipleship",
    "categories": ["Christian Living", "Discipleship"],
    "coverFile": "covers/beauty_for_ashes.jpg",
    "totalPages": 64,
    "totalLines": 1180
  }
]
```

#### Table of Contents
* **URL**: `GET /books/{book_id}/toc.json`
* **Example**: `/books/beauty_for_ashes/toc.json`
```json
{
  "id": "beauty_for_ashes",
  "title": "Beauty for Ashes",
  "chapters": [
    {
      "chapterIndex": 1,
      "title": "Beauty For Ashes",
      "startLine": 1,
      "endLine": 142,
      "startPage": 1,
      "endPage": 6
    }
  ]
}
```

#### Chapter Content Lines
* **URL**: `GET /books/{book_id}/chapters/{chapter_index}.json`
* **Example**: `/books/beauty_for_ashes/chapters/1.json`
```json
[
  {
    "line": 1,
    "page": 1,
    "text": "Beauty For Ashes",
    "contentType": "chapter_header",
    "isHeading": true,
    "headingLevel": 1
  },
  {
    "line": 2,
    "page": 1,
    "text": "God wants to give us beauty for ashes in our lives...",
    "contentType": "p",
    "isHeading": false,
    "headingLevel": 0
  }
]
```

---

### 3. Verse-by-Verse Commentaries

Expositions extracted from Zac Poonen's published books, indexed by Bible passage.

* **URL**: `GET /commentaries/{book_number}/{chapter}.json`
* **Example**: `/commentaries/43/17.json` (Commentary on John 17)
```json
{
  "23": [
    {
      "bookId": "a_godly_family_life",
      "bookTitle": "A Godly Family Life",
      "chapterIndex": 1,
      "chapterTitle": "Introduction",
      "pageNumber": 1,
      "startLine": 4,
      "endLine": 4,
      "headline": "Introduction"
    }
  ]
}
```

---

### 4. Cross-References (TSK Dataset)

Treasury of Scripture Knowledge with 344,000+ cross-reference pairs and relevancy scores.

* **URL**: `GET /cross_references/{book_number}/{chapter}.json`
* **Example**: `/cross_references/43/14.json`
```json
[
  {
    "v": 27,
    "refs": [
      { "b": 19, "c": 29, "v": 11, "s": 85 },
      { "b": 50, "c": 4, "v": 7, "s": 90 }
    ]
  }
]
```

---

### 5. Words Feed & Daily Devotionals

* **Manifest**: `GET /words_feed/manifest.json` (List of topics and counts)
* **Daily 365 Feed**: `GET /words_feed/daily.json`
* **Topic Feed**: `GET /words_feed/topics/{topic_slug}.json` (e.g. `/words_feed/topics/faith.json`)

---

## 💻 Client Integration Examples

### Dart / Flutter
```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

Future<List<Map<String, dynamic>>> fetchChapter(String version, int book, int chapter) async {
  final url = Uri.parse(
    'https://cdn.jsdelivr.net/gh/rozariopersonal/Christian-Tube-Releases@main/bibles/$version/$book/$chapter.json',
  );
  final response = await http.get(url);
  if (response.statusCode == 200) {
    final List<dynamic> jsonList = jsonDecode(response.body);
    return jsonList.cast<Map<String, dynamic>>();
  }
  return [];
}
```

### JavaScript / TypeScript
```typescript
async function fetchVerseCommentary(bookNumber: number, chapter: number) {
  const url = `https://cdn.jsdelivr.net/gh/rozariopersonal/Christian-Tube-Releases@main/commentaries/${bookNumber}/${chapter}.json`;
  const res = await fetch(url);
  return await res.json();
}
```

### Python
```python
import requests

def get_book_toc(book_id: str):
    url = f"https://cdn.jsdelivr.net/gh/rozariopersonal/Christian-Tube-Releases@main/books/{book_id}/toc.json"
    return requests.get(url).json()
```

### cURL
```bash
curl -s https://cdn.jsdelivr.net/gh/rozariopersonal/Christian-Tube-Releases@main/bibles/kjv/43/3.json
```

---

## ⚖️ License & Attribution

- **Bibles**: All included Bible texts are either in the Public Domain (KJV, ASV, BBE, YLT, WEB, TAOBVSI) or published under Creative Commons Share-Alike (CC BY-SA 4.0 by Bridge Connectivity Solutions).
- **Books & Commentaries**: Written by Zac Poonen & Annie Poonen. Used with permission for non-commercial spiritual edification under Christian Fellowship Church (CFC) guidelines.
- **Cross-References**: Derived from the OpenBible.info / HelloAO `open-cross-ref` project (CC BY 4.0).
