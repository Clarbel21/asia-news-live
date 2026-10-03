# Task B — API Calling · Asia News Live 🇸🇬🇭🇰🇮🇩

**▶ Live demo: https://clarbel21.github.io/asia-news-live/**

A visual frontend that displays live news from **Singapore, Hong Kong and Indonesia**, fetched from a **free public API** (no API key, no signup), with the API results shown in **pink text** as required. Switch regions with the tab bar under the header.

## ✅ Task checklist

| Requirement | How it is met |
|---|---|
| 1. Choose a domain | 📰 News — Singapore, Hong Kong & Indonesia top stories (3 regions, one API) |
| 2. Find a free API (read docs) | Google News RSS (local editions) converted to JSON by the free **rss2json** API — no key, no account |
| 3. Make one request, show JSON | Page shows the exact GET URL for the selected region, a "View raw JSON" panel, and a "Download full JSON" button. A saved response is in `sample-response.json` |
| 4. Ask AI to build a visual frontend | This page was AI-built: professional navy/blue dashboard theme, stat cards, animated news cards, region switcher |
| 5. Display API result in pink text | All API-result text — headlines, stat numbers, JSON viewer — is rose-pink (`#ff7bac`); a legend badge on the page explains "pink = live API data" |

## 🔗 The API (free, no key needed)

One pattern, three regional feeds (pick with the tab bar — the GET URL on the page updates automatically):

```
GET https://api.rss2json.com/v1/api.json?rss_url=<encoded Google News RSS URL>
```

| Region | Google News RSS edition | Language |
|---|---|---|
| 🇸🇬 Singapore | `https://news.google.com/rss?hl=en-SG&gl=SG&ceid=SG:en` | English |
| 🇭🇰 Hong Kong | `https://news.google.com/rss?hl=zh-HK&gl=HK&ceid=HK:zh-Hant` | 繁體中文 |
| 🇮🇩 Indonesia | `https://news.google.com/rss?hl=id&gl=ID&ceid=ID:id` | Bahasa Indonesia |

- **Data source**: Google News RSS local editions → aggregates local outlets (Straits Times/CNA; Yahoo HK/明報; detikNews/Kompas…). Note: Google News has no English top-stories edition for HK/ID, so those tabs show the authentic local-language news.
- **Converter**: [rss2json.com](https://rss2json.com) free tier — turns any RSS feed into JSON with CORS enabled, so the browser can call it directly.
- **Resilience**: the free tiers throttle per IP, so the page tries 4 providers in order (rss2json → allorigins → corsproxy.io → codetabs, the last three parse the raw RSS XML client-side), shows which provider served the data, and keeps the last successful response per region in localStorage — if every provider fails, you still see the last cached articles with a clear notice.
- Same call in a terminal: `curl "<URL above>"`

## ▶ How to run

Option 1 — just double-click `index.html` (the API allows browser CORS, so it works straight from disk).

Option 2 — tiny local server:

```bash
cd sg-news
python -m http.server 8931
# open http://localhost:8931
```

## 📸 For the WeChat group share

1. Open the page, wait for news cards to load (status bar shows "✅ OK — N articles received from API").
2. Click "👁 View raw JSON response" so the JSON is also visible, then screenshot.
3. Send the screenshot (optionally with `sample-response.json`) to the group.
