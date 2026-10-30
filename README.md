# Saarthi

Scholarship discovery and mock application demo inspired by the National Scholarship Portal (NSP). It uses synthetic data and never collects real credentials or submits an application.

## Run the interface

Requirements: Node.js 20+.

```sh
npm install
npm run dev
```

## Run the API

Python 3.11+ recommended.

```sh
cd backend
python -m venv .venv
# activate the environment, then:
pip install -r requirements.txt
uvicorn main:app --reload
```

The API is at `http://localhost:8000`; `/docs` shows the Pydantic request and response contracts. For live official-page extraction, install the Chromium browser with `playwright install chromium`, set `GEMINI_API_KEY` (optionally `GEMINI_MODEL`), then POST a profile to `/api/discover`. The current adapter only opens NSP pages and only retains schema-valid Gemini records with evidence URLs. It drops malformed output rather than guessing repairs. Search API integration and broader non-NSP sources remain future work.

The browser UI is self-contained and works without credentials. It includes a portal-style mock login, five application pages (**General Information**, **Financial Details**, **Academic Details**, **Application Specific**, **Applicant Undertaking**), a simulated interruption/recovery prompt, a review screen, and a local-only mock receipt. Select **Open demo application flow** on the discovery page, then acknowledge the mock challenge to continue. Profile values remain in memory. The directory and application form do not call the live API yet.

## Source handling

The demo directory snapshot links to the official [National Scholarship Portal scheme directory](https://scholarships.gov.in/All-Scholarships). AY 2026–27 listings showed a 31 October 2026 student application closing date when this demo was prepared. Scheme amount, eligibility, document requirements, and fresh-versus-renewal distinctions are intentionally marked for verification until read from the relevant official specifications page. The portal's current details may change; always check the source before acting.

## Safety boundaries

- All applicant details shown in the application are synthetic examples.
- The mock login does not request Aadhaar, APAAR, OTR, passwords, or actual OTP/CAPTCHA responses.
- The mock receipt is generated locally and is not an NSP receipt.
- CAPTCHA, OTP, and access-control bypass is out of scope; a real challenge would require the student.
- Real applications are never filled or submitted by this demo.
