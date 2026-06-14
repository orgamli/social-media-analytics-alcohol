# Social Media Analytics – Reddit Discourse Analysis (r/alcohol Network Study)

This project builds an end-to-end analytics pipeline to study alcohol-related discussions on Reddit using API-based data ingestion, graph analytics, and NLP techniques. It collects comment data from r/alcohol, models user interactions as a network, detects communities, and analyses sentiment and topics across them.

---

## Overview

The goal of this project is to analyze how alcohol is discussed online by examining:
- User interaction patterns
- Community structures
- Sentiment dynamics across discussions

Data was collected using the Reddit API and modeled as a user interaction network, where edges represent comment-reply relationships.

---

## Methodology

- **Data Collection**  
  Collected Reddit data using PRAW (Reddit API wrapper)

- **Graph Modeling**  
  Constructed a directed network of user interactions

- **Community Detection**  
  Applied the Louvain algorithm (unsupervised learning) to detect communities

- **Network Analysis**  
  Measured structural properties such as density, clustering, and centrality

- **Text Processing (NLP)**  
  Used spaCy for tokenization, lemmatization, and entity extraction

- **Sentiment Analysis**  
  Applied VADER to evaluate emotional tone across communities

---

## Key Insights

- The interaction network is sparse and hub-driven  
- Distinct communities emerge around different discussion themes:
  - Casual/social drinking  
  - Cocktail and flavor exploration  
  - Brand-focused discussions  
  - Personal effects of alcohol  
- Sentiment varies significantly across communities  
- Influential users (hubs) do not always align with overall community sentiment  

---

## Tech Stack

- Python  
- PRAW (Reddit API)  
- NetworkX + python-louvain (graph analytics & community detection)  
- spaCy (NLP)  
- VADER (sentiment analysis)  
- Matplotlib + WordCloud (visualization)  

---

## Project Structure

```
sma-code.ipynb          Main analysis notebook
requirements.txt        Python dependencies
.env.example            Template for credentials
images/                 Pre-generated output figures
sma-report.docx         Written report
```

---

## How to Run

### 1. Get Reddit API credentials

Create a Reddit app at <https://www.reddit.com/prefs/apps> (choose **script** type).  
You will receive a **client ID** and a **client secret**.

### 2. Set the credentials

**Option A — environment variables (recommended for local Jupyter)**

Copy `.env.example` to `.env`, fill in your values, then export them before launching Jupyter:

```bash
cp .env.example .env
# Edit .env with your credentials, then:
export $(grep -v '^#' .env | xargs)
jupyter notebook sma-code.ipynb
```

Or set them directly in your shell:

```bash
export REDDIT_CLIENT_ID=your_client_id
export REDDIT_CLIENT_SECRET=your_client_secret
export REDDIT_USER_AGENT="SMA_project (by your_username)"
```

**Option B — Google Colab Secrets**

In Colab, open the 🔑 **Secrets** panel (left sidebar) and add the three keys:

| Secret name            | Value                            |
|------------------------|----------------------------------|
| `REDDIT_CLIENT_ID`     | your client ID                   |
| `REDDIT_CLIENT_SECRET` | your client secret               |
| `REDDIT_USER_AGENT`    | `SMA_project (by your_username)` |

The notebook will automatically read from Colab Secrets if the environment variables are not set.

### 3. Install dependencies

```bash
pip install -r requirements.txt
python -m spacy download en_core_web_sm
```

### 4. Run the notebook

Execute the cells top-to-bottom.  
Set `REBUILD_DATA = True` in the configuration cell to re-collect data from Reddit; leave it `False` to reuse the cached CSV.

---

## Notes

- Data collection is capped at 400 posts / 10,000 comments / 5,000 users to keep runtime manageable.
- Community detection uses the Louvain method at resolution 1.0 with a fixed seed (42) for reproducibility.
- Sentiment analysis uses VADER, which is tuned for short, informal social-media text.

---

## Report

A full written report is available in `sma-report.docx`, covering the methodology, findings, and conclusions in detail.
