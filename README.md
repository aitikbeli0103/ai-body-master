# AI Body Master

Needle-free meridian wellness app for in-store use (English / 中文 / Bahasa Malaysia).
Live: https://aitikbeli0103.github.io/ai-body-master/

This is a static website hosted on GitHub Pages. There is no build step and no server code in this repository.

## How it is put together

| File / folder | What it is |
|---|---|
| `index.html` | Small start-up page. Shows a loading screen, asks the server which version of the app is live and opens `app.html?v=<version>` full screen. Same version = the browser re-uses its saved copy (no new 7 MB download); every publish gives a new address, so a new release shows at once. If the version check fails it falls back to a fresh download, so it is never worse than before. Also shows a hint on slow connections and a "Try again" message when there is no internet. |
| `app.html` | The app itself: one bundled page (about 9.8 MB, about 7.4 MB over the network) with all screens (home, Quick Guide, plan flow with the body map, Look up, Knowledge), the fonts and some pictures. |
| `*.json` next to `app.html` | The content: body-part cards per language (`face_symptoms.json`, `.zh.json`, `.ms.json`, and the same for chest, hands, abdomen, feet, legs), Knowledge (`knowledge*.json`), the Look up list (`knowledge_lookup.json`), the assessment lists (`assessment_s2.json`), the video list (`knowledge_videos.json`). |
| `cond/` | One small JSON file per condition (1,852) plus the hero pictures of the condition pages. |
| `personal/` | 13 glass pictures (designed in ChatGPT) used by the Quick Check and My Lookups screens. |
| `sections/`, `knowledge/` | Pictures for the body-part cards and the Knowledge pages. |
| `_ds/` | Two comment-only placeholder files. The app asks for them on every load; without them the browser logs two "404 not found" errors. |
| `app 2.html`, `neck-detail/`, `Login.dc.html` | Old copies that the app does not use (candidates for removal once the owner agrees). |

Languages: the language list and the texts are inside `app.html` and the `*.zh.json` / `*.ms.json` files. The language is not remembered between visits yet.

## Run it on your own computer

```
python -m http.server 8000
```

Then open http://localhost:8000/ . The page must be served over http; opening `index.html` directly from disk does not load the data files.

## What is not part of this app yet

- No accounts, database, file upload, AI service or payments. The Sign In screen is a placeholder (no account is created).
- The numbers on the home screen (name, credit, package, points) and the name on the printed worksheet are sample values.
- The app does not send personal or health information to any server and uses no cookies, analytics or tracking. The only things it remembers are kept in the phone's own browser storage: which of the 5 Quick Check symptoms a person looked at today (3 free checks a day) and their last 50 lookups (`localStorage` keys `abm-qc` and `abm-lookups`). My Lookups has a Clear button that deletes them. Fonts and libraries are bundled inside `app.html`, so it loads nothing from other websites. The "Book" button only opens https://wa.me/ when tapped (no phone number or message is filled in yet).

**This repository is public. Never add customers' health records, personal data, passwords or API keys to it.** Anything that needs private data must live in a separate, access-controlled service.
