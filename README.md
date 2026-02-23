 Markdown
# PodcastSearcherZHTW 🎙️
### *Precision Search Engine for Traditional Chinese Podcast Content*

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![Flask](https://img.shields.io/badge/framework-Flask-black.svg)](https://flask.palletsprojects.com/)
[![Azure](https://img.shields.io/badge/cloud-Azure-0089D6.svg)](https://azure.microsoft.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**PodcastSearcherZHTW** addresses a core limitation in modern podcasting: the inability to search within audio content. By combining automated data ingestion, advanced NLP segmentation, and the **BM25 ranking algorithm**, this system allows users to find specific moments in podcast episodes via a seamless **LINE Bot** interface.

---

## 🏗️ System Architecture

The project utilizes a decoupled, microservices-oriented architecture designed for scalability and low-latency retrieval.



> [!TIP]
> **Recommended Diagram Labels:** > `RSS Feed` ➔ `Azure Functions` ➔ `Blob Storage` ➔ `Jieba NLP` ➔ `Cosmos DB` ➔ `LINE API`

### Key Components:
* **Data Ingestion (Azure Functions):** A serverless pipeline that monitors RSS feeds, fetches transcripts/metadata, and stores raw data in Azure Blob Storage.
* **Indexing Engine:** An NLP processor using `Jieba` (optimized with Traditional Chinese dictionaries) to perform tokenization, stopword removal, and weight calculation.
* **Storage Layer:** * **Azure Cosmos DB:** Manages structured indices and user conversation states.
    * **Azure Blob Storage:** Acts as a data lake for raw transcript files.
* **Backend API (Flask):** The central hub handling LINE Webhooks, executing search queries, and managing dialogue flow via the Microsoft Bot Framework.

---

## 🔥 Technical Highlights

### 🔍 Advanced Information Retrieval
* **BM25 Ranking:** Unlike simple keyword matching, the system implements the **Okapi BM25** algorithm to rank episodes. It calculates scores based on:
    $$score(D, Q) = \sum_{q \in Q} IDF(q) \cdot \frac{f(q, D) \cdot (k_1 + 1)}{f(q, D) + k_1 \cdot (1 - b + b \cdot \frac{|D|}{avgdl})}$$
    This ensures that the most contextually relevant content appears at the top.
* **NLP for ZHTW:** Custom dictionary integration for `Jieba` to handle podcast-specific slang and contemporary Traditional Chinese vocabulary.

### 📱 Intelligent UI/UX
* **Rich Interaction:** Leverages LINE **Carousel Templates** and **Flex Messages** to present search results with episode art, snippets, and direct links.
* **Stateful Dialogues:** Implements a robust state machine to track user search history and profile preferences for personalized results.

---

## 🌅 Project Structure

```text
├── podcast_linebot/        # Core Bot logic & state management
│   ├── bots/               # Dialog Bot implementations
│   ├── dialogs/            # Search logic & User Profile flows
│   └── helpers/            # Bot Framework utility classes
├── podcast_downloader/     # Azure Functions for cloud-based scraping
├── algorithm_test/         # Accuracy evaluation (Precision/Recall) & NLP tuning
└── render_test_linebot/    # Webhook testing & UI template prototyping
🚀 Getting Started
Prerequisites

Python 3.9+

Azure Subscription (Cosmos DB, Blob Storage, Functions)

LINE Developers Account (Messaging API access)

Installation

Clone the Repository:

Bash
git clone https://github.com/yourusername/PodcastSearcherZHTW.git
cd PodcastSearcherZHTW
Configure Environment:
Create a .env file in the root directory:

Code snippet
LINE_CHANNEL_SECRET=your_secret
LINE_CHANNEL_ACCESS_TOKEN=your_token
COSMOS_CONNECTION_STRING=your_cosmos_link
Deploy & Run:

Bash
pip install -r podcast_linebot/requirements.txt
python podcast_linebot/app.py

## 🌻 Roadmap

### ✅ Phase 1: Core Engine (Completed)
- [x] **Automated Data Pipeline:** Implemented Azure Functions for serverless RSS feed monitoring and data ingestion.
- [x] **Advanced Search Algorithm:** Integrated **BM25** ranking to ensure high-relevance retrieval of podcast transcripts.
- [x] **NLP Optimization:** Leveraged `Jieba` with custom Traditional Chinese dictionaries for precise segmentation.
- [x] **LINE Bot Interface:** Developed an interactive UI using Carousel and Flex Messages for mobile-first search.

### 🚀 Phase 2: Intelligence & Expansion (In Progress)
- [ ] **RAG Integration:** Deploy LLMs (OpenAI/Gemini) to provide "TL;DR" summaries of search results.
- [ ] **Automated STT:** Integrate OpenAI Whisper to generate transcripts for podcasts that do not provide them.
- [ ] **Semantic Search:** Implement vector embeddings for "meaning-based" retrieval beyond keyword matching.