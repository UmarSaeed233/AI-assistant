# AI-assistant
# 📄 ATS Resume Checker

A Streamlit app that scores a resume for Applicant Tracking System (ATS) friendliness and tells you exactly how to improve it, powered by Google's Gemini Flash models.

## Features

- Upload a resume as **PDF, DOCX or TXT**
- Optionally paste a **job description** for targeted keyword matching
- **ATS score (0-100)**, a blend of:
  - *Rule-based checks* (35%): contact info, standard sections, length, bullets, dates
  - *Gemini AI analysis* (65%): keywords/relevance, content quality, impact & achievements, readability
- Strengths, weaknesses and **missing keywords**
- Prioritised **improvements** and **rewritten bullet points**
- Downloadable Markdown report

## Project structure

```
ats-resume-checker/
├── app.py            # Streamlit app (UI + logic)
├── requirements.txt  # Python dependencies
├── README.md
└── .gitignore
```

## Run locally

1. Get a free Gemini API key: https://aistudio.google.com/apikey
2. Set up and run:

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt

export GEMINI_API_KEY="your-key"  # Windows PowerShell: $env:GEMINI_API_KEY="your-key"
streamlit run app.py
```

You can also skip the environment variable and paste the key into the app's sidebar.

Alternatively, create `.streamlit/secrets.toml` (already git-ignored):

```toml
GEMINI_API_KEY = "your-key"
# GEMINI_MODEL = "gemini-3.8-flash"   # optional
```

## Choosing the Gemini model

The default model is set by `DEFAULT_MODEL` in `app.py` and can be overridden by the `GEMINI_MODEL` secret/env var or the sidebar field. Model names change often, so if you see "Model not found", check https://ai.google.dev/gemini-api/docs/models and enter a current Flash model (for example `gemini-2.5-flash`).

## Deploy on Streamlit Community Cloud

1. Push this folder to a GitHub repository (see below).
2. Go to https://share.streamlit.io and sign in with GitHub.
3. Click **Create app** → choose your repo, branch `main`, main file `app.py`.
4. Open **Advanced settings → Secrets** and add:
   ```toml
   GEMINI_API_KEY = "your-key"
   ```
5. Click **Deploy**.

## Push to GitHub

```bash
git init
git add .
git commit -m "Initial commit: ATS resume checker"
git branch -M main
git remote add origin https://github.com/<your-username>/ats-resume-checker.git
git push -u origin main
```

Create the empty repository on GitHub first (no README/license, since you already have them). **Never commit your API key.**

## Privacy

Resume text is sent to the Gemini API for analysis and is not stored by this app. Don't upload documents you aren't comfortable sending to a third-party API.

## Limitations

- Scanned/image-only PDFs can't be read (an ATS can't read them either).
- The AI portion is an estimate; real ATS systems differ. Treat the score as guidance, not a guarantee.
