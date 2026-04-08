# Social Media Analytics – Reddit Discourse Analysis

This project builds an end-to-end analytics pipeline to study alcohol-related discussions on Reddit using API-based data ingestion, graph analytics, and NLP techniques.

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
  Applied Louvain algorithm (unsupervised learning) to detect communities

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
- Google Colab  
- PRAW (Reddit API)  
- NetworkX  
- spaCy  
- VADER Sentiment Analysis  
- Matplotlib  

---

## How to Run

1. Open sma-code.ipynb in Google Colab  
2. Set up Reddit API credentials:
  - Go to reddit.com/prefs/apps and create a new app
  - Copy your [client_id] and [client_secret]
  - Update these values in the notebook where PRAW is initialized
3. Install dependencies:
     !pip install praw spacy networkx matplotlib vaderSentiment

## Report
A full written report is available in sma-report.docx, covering the methodology, findings, and conclusions in detail.
