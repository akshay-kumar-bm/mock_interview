# Mock Interview / Visa Interview Coach

A voice-driven interview practice tool. It asks questions aloud, listens to your spoken answer, and gives short spoken feedback using Gemini, then moves to the next question.

## Features
- Text-to-speech questions (`pyttsx3`; the Streamlit version also plays generated audio).
- Speech-to-text answers (`SpeechRecognition`, Google recognizer, microphone via PyAudio).
- Conversational feedback (60-80 words: one strength, one improvement, transition to next question) from `gemini-2.0-flash` through LangChain.
- Chat memory persisted in SQLite (`memory.db`) via `SQLChatMessageHistory` + `RunnableWithMessageHistory` (in `app_memory.py` / `app_new.py`).
- Streamlit UI (`app_new.py`, "Visa Interview Coach") with start / next question / download responses (`interview_responses.json`).

## Three iterations in the repo
| File | What it is |
|---|---|
| `app.py` | Console version, visa interview questions, no memory |
| `app_memory.py` | Console version with SQLite chat history, ML-engineer interview questions |
| `app_new.py` | Streamlit UI, visa questions, memory, saved responses |

## Tech stack
Python, Streamlit, LangChain (`langchain-google-genai`, `langchain-community`), Google Gemini, pyttsx3, SpeechRecognition, PyAudio, pygame, SQLite.

## Setup
```
pip install -r requirements.txt
```
Create a `.env` with `GOOGLE_API_KEY=<your key>`. Then:
```
streamlit run app_new.py     # UI
python app.py                # console
```
A working microphone and speakers are required.

## Limitations
- Question lists are hard-coded; three overlapping scripts rather than one app.
- Local-only audio (mic/pyttsx3), so not deployable to a server as-is.
- Generated artifacts (`memory.db`, `temp_speech.mp3`, `interview_responses.json`) are committed.
