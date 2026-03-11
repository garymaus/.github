# AxonIntegrity Coding Standards & AI Assistant Instructions

## Project Context
- **Company:** Axon Integrity, LLC
- **Mission:** Data integrity & AI infrastructure for hyperscalers, AI labs, data centers
- **Phase 1:** Purple Squirrel talent sourcing with Axon Trust-Mark verification
- **Phase 2:** Integrity Ledger API, IaaA service, Verified Dataset Streaming
- **Phase 3:** Axon Edge Sensors, Integrity-Verified Data Vaults

## Tech Stack
- **Backend:** Python 3.12, FastAPI, Gunicorn, Uvicorn
- **Frontend:** Jinja2 templates, modern CSS (no heavy frameworks)
- **Database:** PostgreSQL (production), SQLite (development)
- **Deployment:** Ubuntu 24.04 LTS VPS, Nginx, systemd, Let's Encrypt SSL
- **Version Control:** Git, GitHub (github.com/garymaus)

## Coding Principles
1. **Minimal Impact:** Only modify code directly related to the task
2. **Use Existing Code:** Always check for existing implementations before writing new code
3. **Windows Compatibility:** Use relative paths, `pathlib.Path`, test on Windows
4. **Error Handling:** Log to `logs/` directory with timestamps, never fail silently
5. **Data Integrity:** Cryptographic signing, provenance tracking, chain of custody
6. **Security First:** No hardcoded credentials, use `.env` files, validate all inputs

## Repository Structure
axonintegrity-platform/ # Main web application ├── src/ # FastAPI application │ ├── app.py # Main application entry │ ├── routes/ # API endpoints │ ├── services/ # Business logic │ └── models/ # Data models ├── templates/ # Jinja2 HTML templates ├── static/ # CSS, JS, images ├── data/ # Data files (gitignored) ├── logs/ # Application logs (gitignored) ├── .env.example # Environment variables template ├── requirements.txt # Python dependencies └── README.md # Project documentation

purple-squirrel-automation/ # Talent sourcing pipeline ├── parsers/ # JD/requirement parsers ├── searchers/ # GitHub/LinkedIn scrapers ├── scorers/ # Candidate scoring logic ├── integrity/ # Axon Trust-Mark verification └── outreach/ # Automated outreach

integrity-ledger/ # Phase 2: Blockchain/provenance axon-trust-mark/ # Certification logic


## AI Assistant Instructions

### When Starting a New Session
1. Read this file first
2. Check `tasks/todo.md` for current priorities
3. Review `tasks/lessons.md` for past mistakes
4. Ask clarifying questions before making assumptions

### Code Generation Rules
- Use type hints for all Python functions
- Add docstrings to all public functions
- Include error handling with specific exceptions
- Log important operations
- Write tests for critical business logic
- Use environment variables for configuration

### Data Integrity Requirements
- All candidate data must be cryptographically signed
- Track provenance (source, timestamp, verification method)
- Implement "chain of custody" for data transformations
- Add integrity scores to all outputs

### Deployment Standards
- Test locally before deploying to VPS
- Use systemd for service management
- Configure Nginx reverse proxy
- Enable SSL/TLS with Let's Encrypt
- Set up log rotation
- Document deployment steps

## Environment Variables
```bash
# Required for all environments
SECRET_KEY=<generated-secret>
ENVIRONMENT=development|production
DEBUG=true|false

# Phase 1: Talent Sourcing
GITHUB_TOKEN=<github-api-token>
LINKEDIN_API_KEY=<linkedin-api-key>
OPENAI_API_KEY=<openai-api-key>

# Phase 2: Data Integrity
INTEGRITY_LEDGER_URL=<blockchain-node-url>
SIGNING_KEY=<private-key-for-signing>

# Production
WEBHOOK_BASE_URL=https://axonintegrity.com
PUBLIC_BASE_URL=https://axonintegrity.com