# Internship Radar — routine instructions

This file is the prompt the daily routine runs with. The routine itself lives at
https://claude.ai/code/routines; this copy is kept here for reference and editing.
If you change this file, also paste the new text into the routine's prompt.

---

You are running the "Internship Radar" search (runs every 4 days) for Fedi Afli. Do the whole job
yourself, start to finish, without asking questions: nobody is watching this run.

## 1. Who the candidate is

- Final-year engineering student looking for a PFE (end-of-studies) internship.
- Duration: 4 to 6 months. Start: January or February 2027 (a start in Dec 2026 or
  March 2027 is acceptable if flexible).
- Fields (any of these): AI, machine learning, deep learning, data science, data
  engineering, big data, computer vision, NLP / LLMs.
- Skills: Python, machine learning / deep learning, data engineering, big data
  (Spark, Hadoop), Java, web development.
- Languages: French and English (also Arabic). Skip postings that require German,
  or any language other than French/English/Arabic.
- Nationality: assume Tunisian. For postings outside Tunisia, say whether the
  posting mentions visa sponsorship or is open to international students; do not
  drop a posting only because it is silent on visas.
- Paid or unpaid both OK; show the stipend when listed.
- Remote and hybrid are OK; mark them.

## 2. Find what was already sent

Use the Gmail connector. Search sent mail with
`in:sent subject:"Internship Radar" newer_than:120d` and read each thread with
`get_thread`. Collect every posting URL in those emails. These are "already sent":
never include them again (also skip the same company + same role title even if
the URL differs).

## 3. Search, three regions in parallel

Launch three subagents at once (Agent tool), one per region. If subagents are not
available, search the regions one after another yourself.

- **Tunisia** (Tunis, Sfax, Sousse, remote-from-Tunisia): LinkedIn, Tanitjobs,
  Keejob, Emploitunisie, Optioncarriere, company career pages (InstaDeep, Vermeg,
  Sofrecom, Talan, Sopra HR, Expensya, Proxym, Telnet, Orange Tunisie,
  Ooredoo, ST Microelectronics Tunisia, Capgemini Tunisia…).
- **Europe** (France first, then Belgium, Luxembourg, Switzerland, Netherlands,
  Spain, Italy, Portugal, Ireland, Nordics; skip German-speaking-only roles):
  Welcome to the Jungle, LinkedIn, Indeed, JobTeaser, HelloWork, company career
  pages (big tech, AI labs, banks, consulting firms, startups).
- **Asia** (Japan, South Korea, Singapore, China, Taiwan, Hong Kong, India, UAE,
  Qatar, Saudi Arabia, Malaysia): LinkedIn, Glassdoor, company career pages,
  university/research-lab internship programs (e.g. A*STAR, RIKEN, KAIST, NUS,
  MBZUAI), big tech internship pages.

Each subagent should use WebSearch (search queries in English and French, e.g.
"stage PFE data science 2027", "PFE intelligence artificielle janvier 2027",
"machine learning internship 6 months 2027") and stop once it has 5 verified matches (at most 5 per region). To save tokens, only open (WebFetch) the most promising candidates, about 8 per region at most.

## 4. Verify every posting

For each candidate posting, open the link (WebFetch) and keep it only if:
- the page loads and the posting is still open (not "expired", "closed", "no longer
  accepting applications", 404, or a redirect to a generic jobs page);
- it is an internship / stage / PFE (not a full-time job, not a 2-month summer
  internship);
- duration and start date fit section 1 (or are not stated and plausibly fit);
- the field fits section 1;
- it is not in the already-sent list.

Prefer the original company/careers page link over aggregator links when both exist.

## 5. Rank and mark urgency

Today's date is the date of this run. Mark a posting **URGENT** if its application
deadline is within 14 days. Sort: URGENT first, then best fit. Keep at most 15
postings total (5 per region).

## 6. Send ONE email

Send with the Gmail connector's `send_message`:
- to: `f3diafli@gmail.com`
- subject: `Internship Radar — <YYYY-MM-DD> — <N> new postings` (use
  `Internship Radar — <YYYY-MM-DD> — no new postings` when there are none)
- `htmlBody` as clean HTML, plus a plain-text `body` alternative.

Email content:
1. A 2–3 line summary: how many new postings per region, how many urgent.
2. Then grouped by region (Tunisia, Europe, Asia), one entry per posting:
   - **[URGENT]** tag if applicable, role title, company, city/country
   - duration, start date, deadline (or "not stated"), paid/unpaid, remote/hybrid/on-site
   - for abroad: visa/international note
   - one line on why it fits (skills/field match)
   - the direct link (clickable)
3. A last line: "Pause or edit this routine at https://claude.ai/code/routines".

Always send the email, even when there are no new postings (then say which
sources were searched), so the candidate knows the routine ran.

If the Gmail connector is not available in this run, do not stop silently: finish the search and put the full digest in your final message instead.

## 7. Finish

Do not commit, push, or open pull requests. End with a one-paragraph summary of
what was sent.
