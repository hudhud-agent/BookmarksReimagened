# BookmarksReimagened

Single-page bookmark manager. Data lives in `bookmarks.json`; the app fetches it from
GitHub raw and renders it as cards. Live site: https://hudhud-agent.github.io/BookmarksReimagened/

## How to add a new bookmark

1. Add a new object to the `bookmarks.json` array (order matters — append at the end).
2. Use this exact shape:

```json
{
  "title": "Short, human-friendly name",
  "url": "https://example.com",
  "desc": "One line describing what the site does.",
  "tags": ["tools", "pdf"]
}
```

### Field rules

- `title` — required. Short, descriptive. Match the site's actual name (not a made-up one).
- `url` — required. Full `https://` URL, exactly as given. Do not add trailing slashes unless the original has them.
- `desc` — required. One clear sentence, accurate to what the site actually does. If unsure, say so instead of guessing.
- `tags` — optional array of lowercase words. Reuse existing tags where possible (`tools`, `pdf`, `design`, `news`, `privacy`, `dns`, `ocr`, `download`, `chat`, `calculator`, `colors`, `powerbi`). Add a new tag only if none fit.
- `icon` — optional. Only set when the site's auto-fetched favicon is wrong or blocked:
  - Use a self-contained `data:image/svg+xml,...` SVG (green background + white glyph for brand icons).
  - NEVER use `static.whatsapp.net` or other hotlink-protected URLs — they return 403.
  - Example for WhatsApp:
    `"icon": "data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 64 64'%3E%3Crect width='64' height='64' rx='14' fill='%2325d366'/%3E%3Cpath d='...' fill='%23fff'/%3E%3C/svg%3E"`

## After editing

1. Validate JSON: `python3 -m json.tool bookmarks.json`
2. Commit and push:
   ```bash
   git add bookmarks.json
   git commit -m "Add <site name> bookmark"
   git push
   ```
3. Confirm the change is live: `curl -s https://raw.githubusercontent.com/hudhud-agent/BookmarksReimagened/main/bookmarks.json` (takes ~1 min to propagate to the site).

## House rules

- The repo is public — never commit secrets, personal phone numbers in full, or anything sensitive.
- Don't modify `index.html` unless specifically asked.
- Titles/descriptions must be truthful, not inferred guesses.