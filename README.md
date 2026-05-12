# AI Resume Screener Agent
### Powered by Groq (LLaMA 3.3-70B) + n8n Workflow Automation

![Status](https://img.shields.io/badge/Status-Live-brightgreen)
![Model](https://img.shields.io/badge/LLM-LLaMA%203.3--70B-orange)
![Platform](https://img.shields.io/badge/Platform-n8n-blue)
![API](https://img.shields.io/badge/API-Groq-red)

---

## Problem Statement

Recruiters spend **6–8 seconds** screening one resume. Companies with 500+ applicants per job post waste hundreds of hours manually matching resumes to job descriptions.

**This AI agent automates that entire process in under 3 seconds.**

---

##  What It Does

An intelligent AI agent that takes a **Resume** + **Job Description** as input and instantly returns:

-  **Match Score** (0–100) — how well the candidate fits
-  **Matched Skills** — skills present in both resume and JD
-  **Missing Skills** — gaps the candidate needs to fill
-  **Strengths Summary** — 2-line AI-generated insight
-  **Verdict** — Strongly Recommended / Recommended / Not Recommended

---

##  Architecture

```
User Input (Chat)
      │
      ▼
┌─────────────────┐
│  Chat Trigger   │  ← n8n Chat Interface
│    (n8n)        │
└────────┬────────┘
         │
         ▼
┌─────────────────────────────────┐
│       AI Agent Node             │
│  ┌─────────────────────────┐   │
│  │  System Prompt:         │   │
│  │  "Expert Resume         │   │
│  │   Screener"             │   │
│  └─────────────────────────┘   │
│                                 │
│  Chat Model: Groq               │
│  (LLaMA 3.3-70B-Versatile)     │
│                                 │
│  Memory: Conversation Buffer    │
└─────────────────────────────────┘
         │
         ▼
┌─────────────────┐
│  JSON Output    │  ← Structured Response
│  match_score    │
│  matched_skills │
│  missing_skills │
│  strengths      │
│  verdict        │
└─────────────────┘
```

---

##  Sample Output

**Input:**
```
RESUME: ECE Student | Python | IoT | ESP8266 | n8n | MATLAB

JOB DESCRIPTION: Python Developer with automation and IoT experience
```

**Output:**
```json
{
  "match_score": 80,
  "matched_skills": ["Python", "IoT"],
  "missing_skills": ["automation skills", "AI/ML knowledge"],
  "strengths": "Strong Python and IoT foundation with hands-on n8n automation experience.",
  "verdict": "Recommended"
}
```

---

##  Tech Stack

| Component | Technology |
|-----------|-----------|
| Workflow Automation | n8n (Cloud) |
| LLM | LLaMA 3.3-70B-Versatile |
| AI API | Groq Cloud (Free tier) |
| Memory | n8n Buffer Window Memory |
| Interface | n8n Chat Trigger |

---

##  How to Run This Locally

### Prerequisites
- n8n account (cloud or self-hosted)
- Groq API Key (free at [console.groq.com](https://console.groq.com))

### Steps

**1. Import the workflow**
```
n8n → New Workflow → Import → Upload: Build_your_first_AI_agent.json
```

**2. Add Groq credentials**
```
Groq Chat Model node → Credentials → Create New → Paste API Key
```

**3. Activate & Test**
```
Click "Open Chat" → Paste Resume + JD → Get instant analysis!
```

---

##  How to Use

Paste this format in the chat:

```
RESUME:
[Your resume text here]

JOB DESCRIPTION:
[JD text here]
```

The agent returns a structured JSON with score, skills match, and hiring recommendation.

---

##  Future Upgrades (Roadmap)

- [ ] PDF resume upload support
- [ ] Batch screening (multiple resumes at once)
- [ ] Google Sheets logging of all results
- [ ] Email notification to recruiter
- [ ] Web dashboard with score visualization
- [ ] ATS keyword optimization suggestions

