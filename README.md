# ⚡ Automated Daily AI News Digest

An end-to-end serverless automation pipeline that aggregates daily artificial intelligence headlines from TechCrunch, synthesizes high-signal takeaways using Google Gemini 2.5 Flash, and delivers a formatted HTML morning brief directly to Gmail every day at 8:00 AM IST.

---
## 🚀 1-Click Clone

Clone the entire 4-step workflow directly into your Zapier account:

👉 **[Use the Zapier Template Here](PASTE_YOUR_ZAPIER_TEMPLATE_LINK_HERE)**
---

## 🏗️ Architecture & Pipeline Flow

```text
[ TechCrunch AI RSS Feed ]
            │ (Continuous feed updates)
            ▼
[ Digest by Zapier ]
            │ (Aggregates and holds entries until 8:00 AM IST)
            ▼
[ Google AI Studio (Gemini 2.5 Flash) ]
            │ (Extracts macro trends, top 3 stories, bullet points, and links)
            ▼
[ Gmail Delivery ]
            │ (Sends styled HTML email to subscriber inbox)
  ```
  📋 Quick Setup Matrix
  
 | Step | App | Event | Key Configuration |
| :--- | :--- | :--- | :--- |
| **1. Ingest** | RSS by Zapier | New Item in Feed | **Feed URL:** `https://techcrunch.com/category/artificial-intelligence/feed/`<br>**Trigger on:** Different Guid/URL |
| **2. Batch** | Digest by Zapier | Append Entry and Schedule Digest | **Title:** `daily_ai_brief`<br>**Frequency:** Daily at `8:00 AM`<br>**Timezone:** `Asia/Kolkata` (`+05:30`)<br>**Delete on Release:** `True` |
| **3. Synthesize** | Google AI Studio (Gemini) | Send Prompt | **Model:** `gemini-2.5-flash`<br>**Format:** Clean HTML only (`<h3>`, `<p>`, `<ul>`, `<a>`) |
| **4. Deliver** | Gmail | Send Email | **To:** Your Email<br>**Subject:** `⚡ Daily AI Digest — {{zap_meta_human_now}}`<br>**Body Type:** `html`<br>**Body:** `{{3. Candidates Content Parts Text}}` |

⚙️ Detailed Step Configurations

Step 1: Trigger — RSS by Zapier
Event: New Item in Feed
Feed URL: https://techcrunch.com/category/artificial-intelligence/feed/
What Triggers a New Feed Item?: Different Guid/URL (recommended)

Step 2: Collector & Scheduler — Digest by Zapier
Event: Append Entry and Schedule Digest
Title: daily_ai_brief
Entry:
Title: {{1. Title}}
Summary: {{1. Description}}
Link: {{1. Link}}

Frequency: Daily
Time of Day: 8:00 AM
Timezone: Set Zapier Profile to (GMT+05:30) Kolkata (Release At: 08:00:00+05:30)
Delete Digest on Release: True

Step 3: Intelligence Engine — Google AI Studio (Gemini)
Event: Send Prompt
Model: gemini-2.5-flash

System Instruction:
```You are an executive tech editor writing a daily AI morning brief. Synthesize aggregated stories into high-signal newsletter copy. Always output clean HTML using only <h3>, <p>, <ul>, <li>, <a>, and <strong> tags. Never use markdown code fences, greetings, or conversational filler.```

Prompt:
Synthesize the following aggregated AI stories collected over the last 24 hours into a unified morning digest:
{{2. Current Digest}}
Structure requirements:
<h3>📅 Executive Brief</h3>
<p><strong>Macro Trend:</strong> [2-sentence high-level overview of the day's biggest developments]</p>
<h3>Top Stories</h3>
[Pick the top 3 most impactful stories from the digest above. For each story, provide:]
<p><strong>[Story Headline]</strong></p>
<ul>
  <li>[Key technical or strategic fact 1]</li>
  <li>[Enterprise, market, or societal impact 2]</li>
</ul>
<p><a href="[Insert source link here]" style="color: #1a73e8; text-decoration: none;"><strong>Read Full Story →</strong></a></p>

Step 4: Dispatcher — Gmail
Event: Send Email
To: Your Email Address
From Name: AI Morning Digest
Subject: ⚡ Daily AI Digest — {{zap_meta_human_now}}
Body Type: html
Body: {{3. Candidates Content Parts Text}}
Add signature default: False       

🔒 Prerequisites
Free Zapier account
Free Google AI Studio API Key
Authenticated Gmail accoun
