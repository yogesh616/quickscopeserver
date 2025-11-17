# QuickScopeServer

**Full-stack news & data aggregator API leveraging Node.js, Cheerio, and Puppeteer. Built to scrape, parse, and serve real-time news headlines, summaries, videos, and health/city info from multiple public web sources for consumption by modern React apps.**

## Table of Contents

- [Project Overview](#project-overview)
- [Tech Stack](#tech-stack)
- [API Endpoints](#api-endpoints)
- [Scrapers & Data Modules](#scrapers--data-modules)
- [Setup & Running](#setup--running)
- [Limitations & Shutdown Notice](#limitations--shutdown-notice)
- [Lessons Learned](#lessons-learned)
- [Folder Structure](#folder-structure)

***

## Project Overview

QuickScopeServer is a custom aggregator API designed to collect, summarize, and serve data from various news and info sites (Hindustan Times, Bing News, AajTak, etc.). The server parses headlines, article summaries, live video info, health stats, and city-specific data—originally for a companion React frontend (news app/UI).

Built as a pure backend project for learning, demo, and product prototyping—NO paid third-party APIs used, only direct scraping via Cheerio and Puppeteer.

***

## Tech Stack

- **Node.js** / **Express**: REST API structure, request handling.
- **Cheerio** / **Puppeteer**: HTML parsing, browser emulation, bypassing JS-heavy pages.
- **Axios**: Outbound HTTP requests from backend.
- **Vercel**: Deployment/hosting config (`vercel.json`).
- **Custom modules**: For each target site's HTML structure and data extraction.

***

## API Endpoints

Main REST endpoints (see `Routes/routes.js` for details):

| Endpoint                  | Method | Description                                   |
|---------------------------|--------|-----------------------------------------------|
| `/bing/feed`              | GET    | Latest headlines/stories from Bing News       |
| `/channels`               | GET    | List of news/video/content channels           |
| `/cities`                 | GET    | City-specific health/news info                |
| `/hindustantimes/topics`  | GET    | Hot topics from Hindustan Times               |
| `/hindustantimes/summary` | GET    | Summarizes top stories - may use AI module    |
| `/aajtak/state`           | GET    | State-wise news reports from AajTak           |
| `/aajtak/stateWiseData`   | GET    | Detailed state data from AajTak               |
| `/health`                 | GET    | Latest health updates/news                    |
| `/latest`                 | GET    | Aggregated latest headlines across sources    |
| `/latestVideos`           | GET    | Most recent news video links                  |
| `/search`                 | GET    | Keyword search across stories                 |
| `/summary`                | GET    | AI-generated summary/fallback (experimental)  |

*Some API modules are now broken due to upstream changes. See Limitations.*

***

## Scrapers & Data Modules

Scraper logic is split into modules by source for clarity and maintainability. Key modules:

- **Scraper/Channels/channels.js**:  
  Parses channel names, URLs, and tags across media sites.
- **Scraper/bing/feed.js**:  
  Handles Bing News headline extraction via Cheerio/Puppeteer (browser emulation required for heavy JS sites).
- **Scraper/cities.js**, **Scraper/health.js**:  
  Pulls health/city stats for frontend dashboards/maps.
- **Scraper/HindustanTimes/topics.js**, **Scraper/HindustanTimes/summary.js**:  
  Topic tags and summaries, sometimes using fallback AI logic if article bodies missing.
- **Scraper/aajtak/state.js**, **Scraper/aajtak/stateWiseData.js**:  
  Structured extraction of state-level reports from AajTak.

***

## Setup & Running

1. **Clone repo**  
   ```
   git clone https://github.com/yogesh616/quickscopeserver.git
   cd quickscopeserver
   ```
2. **Install dependencies**  
   ```
   npm install
   ```
3. **Run locally**  
   ```
   node index.js
   ```
   Or configure your chosen cloud/Vercel environment per `vercel.json`.

4. **API usage:**  
   Make `GET` requests to the endpoints listed above. See `/Routes/routes.js` for parameters and sample responses.

***

## Limitations & Shutdown Notice

- **Fragile Scraping:**  
  Most major news sites (Bing, Hindustan Times, AajTak, etc.) periodically change their UI/HTML, deploy anti-bot/CAPTCHA protections, and block non-browser access. As of several months after initial launch, most endpoints now fail due to these changes.
- **No Paid Proxies:**  
  Project does not use paid proxy services (BrightData, etc.) or custom anti-bot infra—so scraping stability is not maintainable long-term on a $0 budget.
- **API status:**  
  API is now offline/unmaintained, but the codebase remains as a technical demo and educational reference.

***

## Lessons Learned

- Web scraping against major sites is unstable—expect markup changes, anti-bot upgrades, and frequent breakage.
- Stable, production-grade scraping needs proxy rotation, headless browser infrastructure, and continual maintenance.
- Core skills gained: async logic, modular extraction, error handling, express routing, API design, cloud deployment on Vercel.

***

## Folder Structure

```
quickscopeserver/
├── index.js                  # Entry point, Express setup
├── package.json              # Dependencies & scripts
├── vercel.json               # Vercel deployment config
├── Routes/
│   └── routes.js             # Main REST API endpoints
└── Scraper/
    ├── Channels/
    │   └── channels.js       # Channel scraper
    ├── ...
    ├── bing/feed.js          # Bing News scraper
    ├── cities.js             # City data scraper
    ├── health.js             # Health data scraper
    ├── HindustanTimes/
    │   ├── topics.js
    │   └── summary.js
    ├── aajtak/
    │   ├── state.js
    │   └── stateWiseData.js
    ├── latest.js             # Latest headlines
    ├── latestVideos.js       # Latest video links
    ├── search.js             # Keyword search
    └── summary.js            # General summary extraction
```

***

## Demo/Status

**NOTE**: The live API may currently fail due to upstream protection and data changes. Code remains available for study and reference.

***

## Author

[Yogesh Saini](https://github.com/yogesh616)

**Solo-built as a learning, prototyping, and technical showcase for full-stack engineering and the realities of live web data integration.**
