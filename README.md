# Reddit Sentiment & Intent Analyzer (Shill Detector)

An asynchronous data pipeline designed to ingest public Reddit posts based on target keywords, parsing them into structured payloads to analyze user intent and sentiment using the Gemini API. 

This tool is built primarily as a read-only utility to help developers, moderators, and community members identify potential astroturfing, coordinated shilling, and non-organic promotional trends.

---

## 🚀 Key Features

*   **Asynchronous Ingestion:** High-performance, non-blocking data fetching from the Reddit Data API.
*   **Intent Classification:** Leverages **Gemini 2.5 Flash** to look past basic keywords and evaluate actual user intent (e.g., distinguishing a genuine review from a promotional script).
*   **Schema Normalization:** Standardizes chaotic Reddit thread data into a lean, token-efficient JSON payload.
*   **Local Dashboard Compatibility:** Relies on a lightweight FastAPI backend ready to serve structured metrics to a terminal or a web UI.

---

## 🛠️ Tech Stack

| Layer | Technology | Purpose |
| :--- | :--- | :--- |
| **Language** | Python 3.12+ | High-performance backend script execution and AI SDK support. |
| **Framework** | FastAPI | Native `async` engine to manage non-blocking concurrent LLM calls. |
| **Scraper / API** | PRAW (Reddit API) | Robust handling of Reddit’s OAuth2 workflow and rate limiting. |
| **AI Processing** | Gemini 2.5 Flash | Cost-effective linguistic inference with an expansive context window. |
| **Data Format** | JSON / PostgreSQL | Standardized, highly portable schemas suited for document tracking. |

---

## 🔄 System Workflow


```

[Reddit Data API] ──(Async Ingestion)──> [FastAPI Backend] ──(JSON Normalization)──> [Gemini API Inference] ──> [Analytics Dashboard]

```

1.  **Ingestion:** The system queries the Reddit platform for public submissions matching specific user-defined `keywords` within target subreddits, observing a strict `max_results` boundary.
2.  **Extraction:** Raw post payloads are stripped down to core textual and temporal properties (`title`, `body`, `timestamp`, etc.) to minimize API overhead and token consumption.
3.  **Linguistic Analysis:** Normalized datasets are processed by Gemini to output clean sentiment scores and classify whether the underlying text behavior represents organic discussion or potential astroturfing.

---

## 📊 Data Schema

The pipeline maps raw ingestion data into the following strict JSON array structure:

```json
[
  {
    "id": "string",
    "subreddit": "string",
    "title": "string",
    "body": "string",
    "user": "string",
    "timestamp": "string (ISO 8601)",
    "url": "string"
  }
]

```

---

## 🛡️ Platform & Privacy Compliance

This application operates under strict adherence to Reddit's Developer Terms and Responsible Builder Policy:

* **Strictly Read-Only:** The application contains zero functionality for automating posts, comments, private messages, votes, or moderation actions.
* **Transient Inference:** Platform text is processed off-platform transiently via API for real-time sentiment extraction. Data is **never** retained for machine learning model training or fine-tuning.
* **No Personal Profiling:** This tool assesses the linguistic sentiment of public post content relative to an abstract keyword. It does not track, profile, or infer personal, sensitive characteristics of individual platform users.

---

## ⚙️ Setup & Installation (Development)

1. **Clone the Repository**

```bash
   git clone [https://github.com/yourusername/reddit-sentiment-analyzer.git](https://github.com/yourusername/reddit-sentiment-analyzer.git)
   cd reddit-sentiment-analyzer

```

2. **Configure Environment Variables**
Create a `.env` file in the root directory:

```env
   REDDIT_CLIENT_ID=your_reddit_client_id
   REDDIT_CLIENT_SECRET=your_reddit_client_secret
   REDDIT_USER_AGENT=script:sentiment-analyzer:v1.0 (by /u/yourusername)
   GEMINI_API_KEY=your_gemini_api_key

```

3. **Install Dependencies & Run**
*(Note: Implementation scripts are actively undergoing bootstrapping in development).*

```
