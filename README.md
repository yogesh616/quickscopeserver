This repository hosts the backend for a news aggregator application. Built with Express and Cheerio, it scrapes and serves data from multiple news sites




Given your project structure, here’s a README for the backend of your news aggregator application that highlights the scraping and routing functionalities.

News Aggregator Backend
This is the backend for a news aggregator application that scrapes and serves data from multiple news sites. Built with Node.js and Express, the project uses Cheerio for HTML parsing and Axios for HTTP requests to gather information from sources like Aaj Tak, Hindustan Times, and NDTV.

Project Structure
The project is organized as follows:

graphql
Copy code
scrap/
│
├── index.js                # Main server entry point
├── package.json            # Project dependencies and scripts
├── vercel.json             # Vercel deployment configuration
│
├── Routes/
│   └── routes.js           # All Express routes for accessing data
│
└── Scraper/
    ├── aajtak/             # Scraper functions for Aaj Tak
    │   ├── state.js
    │   └── stateWiseData.js
    │
    ├── Channels/           # Additional channel scrapers if needed
    │
    ├── HindustanTimes/     # Scraper functions for Hindustan Times
    │   ├── summary.js
    │   └── topics.js
    │
    ├── cities.js           # Scraper for city-based news
    ├── health.js           # Health-related news scraper
    ├── index.html          # Sample HTML for testing (if applicable)
    ├── latest.js           # Latest news scraper
    ├── latestVideos.js     # Scraper for recent video content
    ├── search.js           # Search feature for news articles
    └── summary.js          # General summary data scraper
Features
Data Scraping: Utilizes Cheerio to parse and extract information from HTML pages.
API Endpoints: Provides endpoints to retrieve specific news categories, city details, search results, videos, and summary data.
Routing: Handles all data requests via Routes/routes.js, organizing API routes for modular use.
Vercel Ready: Configured for deployment on Vercel with vercel.json.

API Endpoints
Here are some of the main routes available in this backend:

/api/cities: Retrieves city-based news.
/api/latest: Fetches the latest news articles.
/api/search: Allows keyword search for articles.
/api/summary: Returns a summary of news articles.
/api/videos: Gets the latest videos.
Endpoints can be modified or extended in Routes/routes.js

Technologies Used
Node.js and Express: For server and routing setup.
Cheerio and Axios: For web scraping and HTTP requests.
Vercel: For deployment.
Contributing
Feel free to fork this repository and submit pull requests if you'd like to contribute to this project.
