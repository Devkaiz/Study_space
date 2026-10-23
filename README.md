# WeatherGPT — SIH 2026 Prototype

WeatherGPT converts verified weather facts into understandable, location-aware disaster advisories. It is an end-to-end React + FastAPI prototype designed to run fully in **DEMO MODE** without any paid API.

## Project structure
```
backend/             FastAPI API, SQLite development fallback, grounded demo services
  app/main.py         Auth, weather, chat, geo targeting, alerts, IVR simulation
  .env.example        Configuration template
frontend/             Vite + React + TypeScript responsive web app
```

## Run
1. Backend: `cd backend; python -m venv .venv; .\.venv\Scripts\Activate.ps1; pip install -r requirements.txt; uvicorn app.main:app --reload --port 8000`
2. Frontend: `cd frontend; npm install; npm run dev`
3. Open `http://localhost:5173`.

## Demo credentials
Mobile: `9999999999` · Password: `Demo@123`.

## DEMO MODE works without credentials
- Weather dashboard and source-labelled realistic demo data
- Deterministic grounded chat with shown weather facts
- Registration/login using PBKDF2 password hashes and local SQLite fallback
- Map polygon and in-region recipient selection
- Emergency simulation, alerts, Malayalam/English advisory, browser speech, IVR/SMS simulation
- Actual measured backend processing timings

## Optional external integrations
`WEATHER_API_KEY` for a weather provider, `OPENAI_API_KEY` for a grounded LLM, `BHASHINI_API_KEY` for regional TTS/translation, and `TELEPHONY_API_KEY` for IVR. None are exposed to the frontend. The current prototype deliberately labels all fallback activity as demo mode.

## SIH demo flow
1. Sign in with the demo account; show Punalur dashboard.
2. Ask “Will it rain tonight?”; show the response and **Weather facts used**.
3. Open Map to show the demo affected polygon and users.
4. Open Admin Demo, choose Malayalam, and click **Simulate Heavy Rainfall**.
5. Show the alert, live log, selected opted-in recipients, voice text / browser playback, IVR DEMO status, and measured timing.
6. Explain that an actual IVR integration delivers normal cellular calls, so the recipient phone does not require an app or mobile internet.

### Architecture notes
Production PostGIS should replace the SQLite bounding-box fallback for robust polygon queries. `GET /atmospheric/demo` documents the xarray spatial/temporal filtering pipeline; add actual NetCDF input and xarray processing when meteorological data is available. Prototype thresholds are demonstrative, not official meteorological thresholds.
