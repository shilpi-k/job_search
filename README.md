# PM Job Finder

A browser-based AI-powered job search tool built for healthcare product managers. Searches for relevant PM openings in real time and generates tailored resumes, cover letters, and outreach messages — all grounded in verified profile facts.

---

## What It Does

**Job Search**
Searches LinkedIn, Indeed, and company career pages for AI Product Manager roles in health tech and health insurance companies. Filters for roles posted within 24 hours, salary above $160K, and remote or Phoenix area locations.

**Document Generation**
For each job found, generates three downloadable DOCX documents:
- Tailored resume aligned to the specific job requirements
- Cover letter with role-specific framing
- LinkedIn outreach message with a concrete question

**Guardrails**
All generated content is grounded in a hardcoded verified profile. The app explicitly prevents Claude from inventing metrics, achievements, or experiences not confirmed in the profile. No fabricated statements.

---

## Built With

- Vanilla HTML, CSS, JavaScript
- [Anthropic Claude API](https://docs.anthropic.com) — job search via web search tool, document generation
- [docx.js](https://docxjs.org) — browser-based DOCX file creation
- Google Fonts — DM Serif Display, DM Sans

---

## How to Use

### Prerequisites

You need access to the Anthropic Claude API. The app calls `https://api.anthropic.com/v1/messages` directly from the browser.

### Run Locally

1. Clone or download this repository
2. Open `pm_job_finder.html` in Chrome or Edge
3. Click **Search Jobs**
4. Wait 15 to 30 seconds for Claude to search job boards
5. Browse results and click any document button to generate and download

### No build step required

This is a single HTML file with no dependencies to install. Open it directly in a browser.

---

## File Structure

```
pm-job-finder/
├── pm_job_finder.html      # Main application file
└── README.md               # This file
```

---

## How It Works

### Job Search Flow

```
User clicks Search
      |
      v
Claude API called with web_search tool
      |
      v
Claude searches LinkedIn, Indeed, company career pages
      |
      v
Results filtered: $160K+, remote/Phoenix, 24 hrs, health tech
      |
      v
Structured JSON returned with job listings
      |
      v
Job cards rendered with match scores
```

### Document Generation Flow

```
User clicks Resume / Cover Letter / Outreach
      |
      v
Job description + verified profile sent to Claude API
      |
      v
Claude generates tailored content using only verified facts
      |
      v
JSON response converted to DOCX using docx.js
      |
      v
File downloaded to user's browser
```

---

## Profile Configuration

The app uses a hardcoded `PROFILE` constant containing verified professional facts. To adapt this app for a different user, update the `PROFILE` object in the `<script>` section:

```javascript
const PROFILE = {
  name: "Your Name",
  email: "your@email.com",
  linkedin: "linkedin.com/in/yourprofile",
  github: "yourgithub.io/project",
  location: "Your City, State",
  summary: "Your professional summary...",
  experience: [...],
  skills: [...],
  education: [...],
  sideProjects: [...]
};
```

Only include facts you can verify and defend in an interview. The document generation prompts instruct Claude to use only these verified facts and not invent anything.

---

## Search Criteria

The app searches for roles matching all of these criteria:

| Filter | Value |
|---|---|
| Role type | AI PM, Senior PM, Staff PM, Principal PM, Technical PM |
| Industry | Health tech, health insurance, healthcare payor |
| Posted | Within last 24 hours |
| Salary | $160,000 or above annually |
| Location | Remote (US) or Phoenix, AZ metro area |

---

## Limitations

- Real-time job availability depends on what Claude can access via web search at the time of query
- Roles posted within exactly 24 hours are best-effort, not guaranteed
- DOCX generation requires the docx.js library to load from unpkg CDN
- API calls are made directly from the browser, requires network access to api.anthropic.com

---

## Related Projects

**CARA — Pre-Adjudication Claims Risk Engine**
An AI-powered tool that scores claims-to-authorization match probability before adjudication, flagging high-risk mismatches for proactive resolution.

Live demo: [shilpi-k.github.io/CARA](https://shilpi-k.github.io/CARA)

---

## Author

**Shilpi Karn**
19 years in US healthcare payor technology. Building AI tools to solve real problems in claims, prior authorization, and member operations.

[linkedin.com/in/shilpikarn](https://linkedin.com/in/shilpikarn) | [shilpi-k.github.io/CARA](https://shilpi-k.github.io/CARA)

---

## License

MIT License. Free to use, adapt, and share.
