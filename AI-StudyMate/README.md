# AI-StudyMate — Local AI Study Assistant

## Overview
AI-StudyMate is a Streamlit study assistant that sends prompts to a locally running Ollama model, `qwen2.5:3b`. It demonstrates study-mode prompt templates, configurable answer length, creativity and token limits, input validation, answer download, local inference, and evaluation of model behaviour.

## Implemented features reported as tested
- Study modes: Explain a Concept, MCQ Quiz, Exam Answer, Summarize Notes, Step-by-Step Learning.
- All three answer-length options.
- Creativity and Maximum New Tokens settings.
- Clear Input.
- Generated-answer download.
- Empty-input validation.
- Local browser-based deployment through Streamlit.

## Environment recorded during testing
- Python 3.14.6
- Streamlit 1.65.0
- Ollama local runtime
- Model: `qwen2.5:3b`
- HTTP request to `http://localhost:11434/api/tags` returned status 200.
- Windows PowerShell; project directory `E:\AI-StudyMate`.

## Requirements and setup
Install Python and Ollama first. In PowerShell:

```powershell
cd E:\AI-StudyMate
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
ollama pull qwen2.5:3b
ollama list
python -c "import requests; print(requests.get('http://localhost:11434/api/tags', timeout=5).status_code)"
streamlit run app.py
```

Open the local URL printed by Streamlit, normally `http://localhost:8501`, and test from the browser. Keep Ollama running while using the app.

If activation is blocked for the current PowerShell session:
```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\.venv\Scripts\Activate.ps1
```

## Evaluation summary
See `test_cases.csv` for test prompts, settings, actual-output summaries, statuses, and observations. The settings column states when exact values were not captured rather than inventing them.

Key results to report honestly:
- T5 **Fail**: the model interpreted “execution unit” as a function/method rather than identifying the intended process-versus-thread comparison.
- T6 **Fail**: the short answer stopped mid-sentence.
- T8 **Pass**: empty input displayed `Please enter a topic, question or notes first.`
- T9 **Partial/Fail**: the answer discussed stock prices but did not clearly disclose the lack of live market-data integration.
- T10 **Fail**: despite calling ZX-900 fictional, the model supplied specific unverified academic references. Do not reuse those references without independent verification.
- Variants A/B/C all produced relevant explanations; A was more technical, B more conversational, and C most directly comparative due to its table.

## Limitations and responsible AI
A small local model may truncate long answers, misunderstand ambiguous prompts, or fabricate details and citations. It has no live market-data access unless a separate data source is integrated. Check generated academic content against course materials and trustworthy sources. Do not present model-generated citations as verified unless they have been checked.

## Possible improvements
1. Detect likely truncation and offer a Continue Answer action.
2. Ensure answer-length settings and Maximum New Tokens are passed to Ollama as intended.
3. Improve mode-specific prompt templates and ambiguous-question handling.
4. Add automated checks for empty input, Ollama unavailable, request timeout, and malformed responses.
5. Strengthen instructions against invented citations and explicitly disclose missing live-data access.
6. Save anonymized test outcomes as CSV.

## Submission evidence checklist
- [ ] Application home screenshot showing title, input, settings and output area.
- [ ] Browser screenshot of a successful generated answer.
- [ ] Terminal screenshot showing Python/Streamlit versions, `ollama list`, and API status 200.
- [ ] Empty-input validation screenshot.
- [ ] Evidence of answer download.
- [ ] Include `requirements.txt`, `test_cases.csv`, and this README.
- [ ] If required, append full outputs/screenshots for every test; the CSV has concise summaries.
- [ ] Do not claim hosted deployment unless you actually deploy and test a hosted URL.
