# ATS Resume Analyzer

A Streamlit app that lets a user upload a resume and receive:

- An estimated ATS compatibility score
- Resume section checks
- Gemini 2.5 Flash feedback
- Priority improvements
- Keywords to consider for a target job
- Formatting and ATS tips

## Files

```text
ats-resume-analyzer/
├── app.py
├── requirements.txt
└── README.md
```

## 1. Get a Gemini API key

Create a Gemini API key in Google AI Studio.

Do **not** put the key directly in `app.py` or commit it to GitHub.

## 2. Run locally

Install Python 3.12 or another currently supported Python version.

```bash
python -m venv .venv
```

Windows:

```bash
.venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Create this local file:

```text
.streamlit/secrets.toml
```

Put this inside:

```toml
GEMINI_API_KEY = "YOUR_GEMINI_API_KEY"
```

Then run:

```bash
streamlit run app.py
```

You can also paste the API key into the app's sidebar while testing locally.

## 3. Push to GitHub using the GitHub website

1. Sign in to GitHub.
2. Click **+** in the top-right corner and choose **New repository**.
3. Give it a name such as `ats-resume-analyzer`.
4. Create the repository.
5. Open the repository and choose **Add file → Upload files**.
6. Upload:
   - `app.py`
   - `requirements.txt`
   - `README.md`
7. Click **Commit changes**.

### Important

Do **not** upload `.streamlit/secrets.toml`. Add it to `.gitignore` if you test locally:

```gitignore
.streamlit/secrets.toml
.venv/
__pycache__/
*.pyc
```

## 4. Deploy on Streamlit Community Cloud

1. Open Streamlit Community Cloud and sign in with GitHub.
2. Click **Create app**.
3. Select your GitHub repository.
4. Select the branch, normally `main`.
5. Set the main file to `app.py`.
6. Open **Advanced settings**.
7. In **Secrets**, paste:

```toml
GEMINI_API_KEY = "YOUR_GEMINI_API_KEY"
```

8. Deploy the app.
9. After deployment, open the generated `streamlit.app` URL and test a resume upload.

## 5. How the score works

The local score is intentionally transparent:

- Up to 60 points: presence of common resume sections.
- Up to 40 points: overlap with terms from the optional job description.

Gemini provides the qualitative review and improvement suggestions.

This is an **estimated ATS compatibility score**, not a score produced by a specific employer's ATS. Real ATS platforms can use different parsing and ranking rules.

## 6. Testing checklist

Before deployment, test:

- PDF upload
- DOCX upload
- TXT upload
- Empty upload
- Resume with no extractable text
- Resume without a job description
- Resume with a job description
- Missing Gemini API key
- Invalid Gemini API key
- Gemini JSON response handling

## 7. Security

Never commit an API key to GitHub. Use Streamlit Secrets for deployed apps and keep local secrets outside version control.
