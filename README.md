# Social Media Analytics — r/alcohol Network Study

A Jupyter/Colab notebook that collects Reddit comment data from r/alcohol, builds a user-interaction network, detects communities with the Louvain algorithm, and analyses sentiment and topics per community.

## Project structure

```
sma-code.ipynb          Main analysis notebook
requirements.txt        Python dependencies
.env.example            Template for credentials
images/                 Pre-generated output figures
sma-report.docx         Written report
```

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

| Secret name           | Value                         |
|-----------------------|-------------------------------|
| `REDDIT_CLIENT_ID`    | your client ID                |
| `REDDIT_CLIENT_SECRET`| your client secret            |
| `REDDIT_USER_AGENT`   | `SMA_project (by your_username)` |

The notebook will automatically read from Colab Secrets if the environment variables are not set.

### 3. Install dependencies

```bash
pip install -r requirements.txt
python -m spacy download en_core_web_sm
```

### 4. Run the notebook

Execute cells top-to-bottom.  
Set `REBUILD_DATA = True` in the configuration cell to re-collect data from Reddit; leave it `False` to reuse the cached CSV.

## Notes

- Data collection is capped at 400 posts / 10 000 comments / 5 000 users to keep runtime manageable.
- Community detection uses the Louvain method at resolution 1.0 with a fixed seed (42) for reproducibility.
- Sentiment analysis uses VADER, which is tuned for short informal social-media text.
