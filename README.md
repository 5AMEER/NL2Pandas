# NL2Pandas

Minimal Streamlit app that converts natural language queries into executable Pandas code using Gemini 1.5 Flash and runs it locally against uploaded Excel data.

## Features
- Excel-only upload (`.xlsx`)
- Two-pane UI (left metadata panel, right chat interface)
- Secure execution guardrails:
  - Forbidden keyword scan
  - `exec` with empty builtins
  - Threaded timeout (10s)
  - Enforced `ans` contract
- Result preview and Excel export
- Debug expander for raw response, cleaned code, and errors

## Project Structure
- `ui.py`: Streamlit entrypoint and UI orchestration
- `nl2pandas/config.py`: app constants and environment settings
- `nl2pandas/data_observer.py`: file loading and metadata extraction
- `nl2pandas/llm.py`: Gemini prompt + generation wrapper
- `nl2pandas/security.py`: markdown stripping, guardrails, safe execution
- `nl2pandas/exporters.py`: Excel export utility

## Setup
```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Set up the `.env` file:
1. Create a `.env` file in the project root:
   ```bash
   touch .env
   ```
2. Add your API key to the `.env` file:
   ```env
   GEMINI_API_KEY=your_api_key_here
   ```

## Run
```bash
streamlit run ui.py
```

## Notes
- Query handling is single-turn (no conversational history).
- Uploaded source DataFrame is kept immutable; execution always uses `df.copy()`.
