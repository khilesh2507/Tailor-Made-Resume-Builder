# Tailor-Made-Resume-Builder
Tailor Made is an AI powered resume optimizer that takes an existing resume and a target job description, and instantly rewrites the resume to maximize ATS compatibility and keyword alignment. Built to operate in seconds with no signup required , it delivers a fully tailored, recruiter ready resume.

## **One Minute Project Overview**

### Problem

Job seekers spend hours manually rewriting their resume for every job application. They struggle to match the exact keywords, tone, and structure that ATS (Applicant Tracking Systems) require. It leads to rejection before a human even reads their resume.

**Context & Realisation:**

I realised that most people have a strong background but struggle to present it in the right format. The resume writing process is repetitive, time-consuming, and highly manual. Every job requires a slightly different version of the same resume and most people simply reuse one generic version. I needed a tool that could instantly tailor any resume to any job description.

**Solution:**

I built Tailor Made: an AI-powered resume optimizer that takes existing resume and a job description, then instantly rewrites the resume to maximize ATS compatibility and keyword alignment. The tool runs in seconds, requires no signup, and delivers a fully tailored, recruiter ready resume.

**Result & Impact:**

Tailor Made reduces resume tailoring time from 2-3 hours to under 30 seconds. It eliminates guesswork around ATS keywords, improves keyword match rate to 80%+, and gives job seekers a competitive edge, all with zero manual effort.

### *if you want to read more, keep scrolling :)*

---

## Problem Statement

As a job seeker or career switcher, tailoring a resume for every application is one of the most frustrating parts of job hunting.

However, the process was completely manual. Every application required to:

- Read the full job description carefully
- Identify the key skills and keywords
- Manually rewrite resume bullets to match
- Worry about whether the ATS would even read it

This process was time consuming, inconsistent, and inefficient.

I wanted a system that could:

- Automatically analyze the job description
- Identify missing keywords and skills
- Rewrite the resume to match the role
- Deliver a clean, ATS optimized output instantly

This would allow job seekers to apply faster and more confidently.

### Key Challenges

- Every job description uses different language and keywords
- ATS systems penalize generic resumes that don't match the role
- Manual rewriting is inconsistent and error-prone
- Most people don't know what ATS looks for
- Existing tools are expensive, slow, or require sign-up

---

## **System Architecture:**
<img width="2000" height="1129" alt="Screenshot 2026-04-22 at 2 26 12 PM" src="https://github.com/user-attachments/assets/c7986866-77f0-40e3-9cb7-f9974071b0a3" />

<img width="1982" height="1127" alt="Screenshot 2026-04-22 at 2 24 32 PM" src="https://github.com/user-attachments/assets/8ec01f64-a875-431b-a2e2-aee7ea438d86" />



### Workflow Overview

- **Frontend (Lovable):** User pastes resume text and job description, clicks Tailor Resume
- **Ngrok:** Tunnels the POST request from Lovable (cloud) to local N8n instance securely
- **Webhook (N8n):** Receives the POST request with resumeText and jobDescription
- **AI Agent (N8n):** Processes inputs with a detailed system prompt and ATS rules
- **LLM (Groq — Llama 3.3 70B):** Rewrites the resume following all formatting and keyword rules
- **Respond to Webhook:** Returns the tailored resume back to the frontend
- **Result Display:** User sees side by side original vs tailored resume with copy button

---

## Implementation Details:

### Data Input

The user provides two inputs via the frontend which is existing resume as plain text or pdf and the target job description. Both are sent via a POST request to the N8n webhook.

The system accepts resumes in any format.

### AI Processing

The AI Agent processes the inputs with a detailed system prompt that includes:

- ATS Safety Rules — no tables, graphics, or special characters
- Keyword & Content Rules — target 80%+ keyword match with the job description
- Formatting Rules — bullet character, word limits, section order
- Output Structure — CONTACT, SUMMARY, SKILLS, EXPERIENCE, EDUCATION, CERTIFICATIONS
- Strict instructions to never invent facts or metrics

### Report Generation & Delivery

The processed output is returned directly to the frontend as clean plain text. The UI then renders it in a structured, readable format with section headers and bullet points.

A side by side comparison view shows the original resume alongside the tailored version, making the improvement immediately visible to the user.

---

## Impact:

### Quantitative Impact

- Reduced resume tailoring time from 2-3 hours to under 30 seconds
- Achieved 80%+ keyword match rate with target job descriptions
- Eliminated manual keyword research and rewriting entirely
- Zero manual intervention after submitting, fully automated end to end
- Works for any industry, role, or experience level

### Qualitative Impact

- Gives job seekers confidence that their resume will pass ATS filters
- Makes resume tailoring accessible to everyone
- Side by side comparison makes improvement immediately visible
- Completely private, no data stored after the session ends
- Built a scalable system that can handle multiple users simultaneously

---

## Challenges & Iterations

### Major Challenges

- Lovable couldn't reach local N8n — Lovable runs on the cloud, N8n was running on my laptop. There was no direct way to connect them
- Ngrok was blocking requests silently — Set up Ngrok to bridge the gap, but every request was getting intercepted by Ngrok's browser warning page and never reaching N8n
- Getting the AI to follow strict formatting rules consistently
- Handling long resumes and job descriptions without losing context
- Managing API rate limits during testing

### How I Solved Them

- **Ngrok as the tunnel** — Used Ngrok to expose my local N8n webhook as a public URL so Lovable could send requests to it
- Wrote a detailed, structured system prompt with explicit rules for every edge case
- Switched from Basic LLM Chain to AI Agent node for cleaner input handling
- Moved from Google Gemini to Groq (Llama 3.3 70B) for better reliability and free tier limit.

---

## The Prompt That Powers It

This is the exact system prompt running inside the AI Agent node in N8n:

<img width="1479" height="1087" alt="prompt_image_simple jpg" src="https://github.com/user-attachments/assets/b96de2fe-cb41-46e0-9ec0-299e7ed562ab" />



---

## Tech Stack

- **Frontend:** Lovable (React) — UI design and deployment
- **Automation:** N8n (self-hosted) — webhook, AI agent, workflow orchestration
- **AI Model:** Groq API — Llama 3.3 70B Versatile
- **Tunneling:** Ngrok — exposing local N8n to the internet
- **Language:** JavaScript (frontend), N8n nodes (no-code backend)
