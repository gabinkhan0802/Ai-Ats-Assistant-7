# Ai-Ats-Assistant-7
# 📄 ATS Resume Checker

Upload a resume (PDF, DOCX or TXT) and get an **estimated ATS score**, a score breakdown,
strengths, prioritized improvements, missing keywords and example bullet rewrites.
Built with **Streamlit** and **Google Gemini Flash**.

> The score is an AI estimate, not an official result. Real ATS tools (Workday, Greenhouse, Lever...) all score differently.

## Features
- PDF / DOCX / TXT upload (reads text inside DOCX tables too)
- Optional job description for targeted keyword matching
- Overall score + 5 categories: formatting, keywords, impact, clarity, completeness
- Improvements sorted High -> Low priority
- Download the report as JSON
- Clear errors for scanned PDFs, bad API key, wrong model name, rate limits

## Run locally
```bash
pip install -r requirements.txt
streamlit run app.py
```
Get a free API key at https://aistudio.google.com and paste it in the sidebar,
or set it as an environment variable: `export GEMINI_API_KEY="your-key"`.

## Model name
The default model is set by `DEFAULT_MODEL` in `app.py`. Google renames and retires models often.
If you see "model not found", type the current Flash model name from
https://ai.google.dev/gemini-api/docs/models into the sidebar box (or set a `GEMINI_MODEL` secret).

---

## Push to GitHub (using the website only)
1. Sign in at https://github.com and click **+** (top right) -> **New repository**.
2. Name it (e.g. `ats-resume-checker`), choose **Public**, leave all the "Add a README / .gitignore / license" options **unticked** (you are uploading your own README), then click **Create repository**.
3. On the empty repo page click **uploading an existing file**.
4. Drag in `app.py`, `README.md` and `requirements.txt` (the file must be named exactly `requirements.txt`).
5. Add a commit message like `Initial commit` and click **Commit changes**.

**Never upload your API key.** Keep it only in Streamlit's Secrets box (below).

## Deploy on Streamlit Community Cloud
1. Go to https://share.streamlit.io and sign in with GitHub (allow access to your repo).
2. Click **Create app** -> **Deploy a public app from GitHub**.
3. Pick your repository, branch `main`, and main file path `app.py`.
4. Click **Advanced settings** -> **Secrets** and paste:
   ```toml
   GEMINI_API_KEY = "your-gemini-api-key"
   ```
   (Optional) add `GEMINI_MODEL = "current-flash-model-name"`.
5. Click **Deploy**. After a minute or two you get a public `*.streamlit.app` link.

To update the app later, edit the file on GitHub (pencil icon) and commit; Streamlit redeploys automatically.

## Privacy
Resumes are sent to Google's Gemini API for analysis and are not stored by this app.
If you share the app publicly, anyone using it spends **your** API quota, so consider leaving the key box empty and letting users enter their own key.
