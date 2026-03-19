# John BP Agent — Healthcare AI Agent

A complete **Agentic AI** healthcare monitoring system that reads patient vitals, analyses risk using Groq AI, and automatically sends WhatsApp alerts to doctors.

## Live Demo
- **API Docs:** https://john-bp-agent.onrender.com/docs
- **Health Check:** https://john-bp-agent.onrender.com/
- **Trigger Agent:** https://john-bp-agent.onrender.com/check/1
## What This Project Does
Hardware/Device → FastAPI → PostgreSQL → AI Agent → Groq AI → WhatsApp Alert

1. Patient vitals (BP, heart rate, oxygen) are stored in PostgreSQL
2. AI Agent reads the vitals and medicines
3. Groq AI (Llama 3.1) analyses the risk level
4. If HIGH or CRITICAL risk → WhatsApp alert sent to doctor automatically
5. All alerts logged to database for audit trail

### Risk Levels Tested
| Risk Level | BP      | Heart Rate | Oxygen | WhatsApp Alert |
|------------|---------|------------|--------|----------------|
| LOW 		 | < 120   | < 70       | > 98%  | No 			  |
| NORMAL 	 | 120–140 | 70–90 		| 95–98% | No 			  |
| HIGH 		 | 140–170 | 90–110 	| 90–95% | Yes 			  |
| CRITICAL   | > 170   | > 110 		| < 90%  | Yes — Immediate|

## Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| API | FastAPI + Python | REST endpoints |
| Database | PostgreSQL (Render) | Store patients, vitals, alerts |
| AI Brain | Groq API (Llama 3.1) | Risk analysis |
| Agent | Pure Python loop | Tool calling without LangChain |
| Alerts | Twilio WhatsApp | Doctor notifications |
| Deployment | Render.com | Live 24/7 hosting |
| Version Control | GitHub | Code management |

## Project Structure

john-bp-agent/
├── main.py              # FastAPI app — API endpoints
├── agent.py             # AI Agent brain — main loop
├── database.py          # PostgreSQL connection + queries
├── groq_client.py       # Groq AI connection
├── tools.py             # 3 agent tools
├── alerts.py            # Twilio WhatsApp sender
├── create_tables.py     # One-time DB setup
├── test_groq.py         # Test Groq API
├── test_db.py           # Test database connection
├── test_whatsapp.py     # Test Twilio WhatsApp
├── .env.example         # Environment variables template
├── .gitignore           # Ignore secrets and venv
├── Procfile             # Render deployment config
└── requirements.txt     # Python dependencies

## Getting Started

### Prerequisites
- Python 3.11+
- PostgreSQL database (Render free tier)
- Groq API key (console.groq.com — free)
- Twilio account (twilio.com — free trial)

### 1. Clone the repository
```bash
git clone https://github.com/amikkili/john-bp-agent.git
cd john-bp-agent
```
### 2. Create virtual environment
```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Mac/Linux
source venv/bin/activate
```
### 3. Install dependencies
```bash
pip install -r requirements.txt
```
### 4. Configure environment variables
```bash
cp .env.example .env
```
Open `.env` and fill in your real values:
```
DATABASE_URL=postgresql://user:password@host:5432/dbname
GROQ_API_KEY=gsk_your_key_here
TWILIO_SID=ACyour_sid_here
TWILIO_TOKEN=your_token_here
DOCTOR_WHATSAPP=whatsapp:+1your_number
```
### 5. Setup database
```bash
python create_tables.py
```
### 6. Test each component
```bash
python test_db.py          # Test database connection
python test_groq.py        # Test Groq AI
python test_whatsapp.py    # Test WhatsApp
```

### 7. Run the app
```bash
uvicorn main:app --reload
Open **http://localhost:8000/docs** to test all endpoints.
```
## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | Health check |
| GET | `/check/{patient_id}` | Trigger agent for a patient |
| POST | `/vitals` | Save new vital reading + trigger agent |
| GET | `/patients` | List all patients |
| POST | `/patients` | Add new patient |

### Example — Trigger agent check
```bash
curl https://john-bp-agent.onrender.com/check/1
```

### Example — Send new vitals (simulate hardware)
```bash
curl -X POST https://john-bp-agent.onrender.com/vitals \
  -H "Content-Type: application/json" \
  -d '{"patient_id":1,"blood_pressure":165,"heart_rate":105,"oxygen_level":92}'
```

---

## How the AI Agent Works
```
run_patient_check(patient_id)
        │
        ▼
Groq AI decides: call check_patient_vitals()
        │
        ▼
Fetches: BP, HR, O2, medicines from PostgreSQL
        │
        ▼
Groq AI decides: call analyse_risk()
        │
        ▼
Returns: RISK_LEVEL, DRUG_CONFLICT, ACTION, URGENCY
        │
        ▼ (if HIGH or CRITICAL)
Groq AI decides: call alert_doctor()
        │
        ▼
WhatsApp sent to doctor + alert saved to DB
        │
        ▼
Agent returns full summary
```

**No LangChain needed** — the agent loop is built with pure Python + Groq's tool calling API. Students can see exactly how agents work internally.

## Test Scenarios

Run these in DBeaver or any PostgreSQL client:

```sql
-- LOW risk
INSERT INTO vitals (patient_id, blood_pressure, heart_rate, oxygen_level)
VALUES (1, 110, 68, 99.0);

-- NORMAL
INSERT INTO vitals (patient_id, blood_pressure, heart_rate, oxygen_level)
VALUES (1, 135, 85, 96.0);

-- HIGH risk (WhatsApp alert)
INSERT INTO vitals (patient_id, blood_pressure, heart_rate, oxygen_level)
VALUES (1, 158, 100, 93.0);

-- CRITICAL (immediate WhatsApp)
INSERT INTO vitals (patient_id, blood_pressure, heart_rate, oxygen_level)
VALUES (1, 185, 122, 88.0);
```

After each INSERT — call `/check/1` to see the agent respond.


## Common Errors and Fixes

| Error | Fix |
|-------|-----|
| `llama3-70b-8192` decommissioned | Use `llama-3.1-8b-instant` |
| Twilio "Invalid From and To pair" | Set `DOCTOR_WHATSAPP=whatsapp:+1XXXXXXXXXX` |
| WhatsApp not received | Send `join your-word` to +14155238886 first |
| GitHub push blocked (secrets) | Remove real keys from `.env.example` |
| LangChain import error | Use the pure Python agent in `agent.py` |

## Deployment

This project is deployed on **Render.com** (free tier).

Every `git push` to `main` triggers automatic redeployment.

```bash
git add .
git commit -m "your change description"
git push
# Render auto-deploys in 2-3 minutes
```

## Environment Variables

| Variable | Description | Where to get |
|----------|-------------|--------------|
| `DATABASE_URL` | PostgreSQL connection string | Render → DB → External URL |
| `GROQ_API_KEY` | Groq AI API key | console.groq.com |
| `TWILIO_SID` | Twilio account SID | twilio.com → Console |
| `TWILIO_TOKEN` | Twilio auth token | twilio.com → Console |
| `DOCTOR_WHATSAPP` | Doctor's WhatsApp number | Your phone number |

## Course Reference

This project is the **Course 1 Capstone** of the Agentic AI series:

- **Free:** Python Fast-Track for Developers (YouTube)
- **Course 1:** Agentic AI — Build Real AI Agents ← This project
- **Course 2:** MLOps — Deploy AI to Production
- **Course 3:** Multi-Agent Systems and MCP

## Author

Built by **Anil Mikkili** — MuleSoft Developer turned AI Specialist

- GitHub: https://github.com/amikkili/john-bp-agent.git

## License

MIT License — free to use for learning and teaching.
