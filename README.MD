# Resume Analyzer

Automated Resume Relevance Analyzer — analyzes and scores a candidate's resume against a job description and provides AI-powered suggestions to improve fit.

Features
- Extracts text from PDF and DOCX job descriptions and resumes
- Extracts and matches key skills (hard keyword matching)
- Computes semantic similarity using sentence embeddings
- Produces a final weighted relevance score and human-friendly verdict
- Generates AI feedback (Gemini) with actionable suggestions
- Stores analysis reports in a local SQLite database and exposes a Streamlit dashboard

Prerequisites
- Python 3.9+
- Internet access (for model downloads and the generative AI API)

Key Python libraries used
- streamlit
- pandas
- python-docx
- PyMuPDF (fitz)
- spacy (and the `en_core_web_sm` model)
- sentence-transformers
- google-generativeai (Gemini client)

Quick Setup
1. (Optional) Create and activate a virtual environment:

	python -m venv .venv
	.venv\Scripts\activate

2. Install required packages:

	pip install streamlit pandas python-docx PyMuPDF spacy sentence-transformers google-generativeai

3. Install the spaCy English model:

	python -m spacy download en_core_web_sm

Running the App
1. From the project root (`Resume_Analyzer/`), run:

	streamlit run app.py

2. Use the sidebar to paste your Google AI API key (the app does not store the key).
3. Go to the "Analyzer" page, upload a Job Description (PDF/DOCX) and a Resume (PDF/DOCX), then click "Analyze Relevance".

Outputs
- Analysis metrics: Final weighted score, keyword match score, semantic similarity
- Skill lists: matched and missing skills
- AI feedback: concise suggestions for improving the resume
- Results saved to a local SQLite DB file: `analysis_results.db`

Project structure
- `app.py` — Streamlit UI and orchestration (uploads, calling analysis functions, saving results)
- `parser.py` — Extracts text from PDF/DOCX files
- `analyzer.py` — Text standardization and skill extraction (spaCy)
- `scorer.py` — Hard-match scoring and semantic similarity (sentence-transformers)
- `feedback.py` — Generates AI feedback using Google generative AI (Gemini)
- `database.py` — Simple SQLite helper for saving/fetching results
- `uploads/jds/` — Stored uploaded job descriptions
- `uploads/resumes/` — Stored uploaded resumes

Notes & Troubleshooting
- Provide a valid Google AI API key in the sidebar to enable AI feedback. If the key is missing or invalid, feedback generation will fail gracefully.
- The first run may download ML models (spaCy, sentence-transformers) which can take time and require internet access.
- Supported file formats for uploads: `.pdf`, `.docx`.
- If you see errors extracting text from PDFs, verify `PyMuPDF` (`fitz`) is installed and the PDF is not corrupted.

Extending the project
- Add more skills to `SKILL_LIST` in `analyzer.py` to improve hard-match coverage.
- Swap or fine-tune the sentence-transformers model in `scorer.py` for domain-specific similarity.

License
This repository contains example code — adapt and extend as needed.

