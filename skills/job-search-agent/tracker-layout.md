# Tracker layout (used by "Set up my job search")

Create these tabs in this order, in one Google Sheet named **Job Search Tracker**. Row 1 of every tab is the header,
bold, white text on dark blue (`#1F3A5F`), frozen. Both skills read and write these tabs by column position, so the
headers must match exactly.

## Tabs and headers

| Tab | Headers (row 1, from column A) |
|---|---|
| Start Here | (no header – see "Start Here text" below) |
| Summary | Metric, Count |
| Job Leads | #, Date Found, Country, Company, Role, Location, Work Mode, Seniority, Posted Salary, Fit Score, Why It Fits, Work-Rights Evidence, Requirements, Job Link, Source, Lead Status, Posted/Closing, Agent Notes, Matched, Gaps, Risks, Your Skip Reason, Cover Letter Draft, LinkedIn Note |
| Applications | #, Date Applied, Country, Company, Role, Location, Work Mode, Type, Posted Salary, Salary Asked, Applied Via, Job Link, Recruiter/Contact, Outreach, Work-Auth Notes, Cover Letter, Status, Follow-up Date, Notes |
| Reviewed - Not Applied | Date Reviewed, Country, Company, Role, Location, Reason Skipped, Job Link |
| Seen - Not Added | Date Seen, Country, Company, Role, Job Link, Reason, Seen By |
| Watchlist | country, company, priority, cities, careers_url, feed_url, feed_type, work_rights_evidence, last_scanned, feed_status, notes |
| Markets | Country, Work-rights route, Job boards, Search keywords, Cities, Notes |
| Agent Learnings | Country, Learnings, Last Updated |
| Agent Runs | Date, Agent, Count 1, Count 2, Summary, Log |
| Settings | Setting, Value, What it is |

## Summary tab (A2:B14, formulas)

| Metric | Count |
|---|---|
| Leads – New | `=COUNTIF('Job Leads'!P:P,"New")` |
| Leads – Shortlisted | `=COUNTIF('Job Leads'!P:P,"Shortlisted")` |
| Leads – Applied | `=COUNTIF('Job Leads'!P:P,"Applied")` |
| Leads – Skipped | `=COUNTIF('Job Leads'!P:P,"Skipped")` |
| Leads – Expired | `=COUNTIF('Job Leads'!P:P,"Expired")` |
| Applications – Applied | `=COUNTIF(Applications!Q:Q,"Applied")` |
| Applications – Under Review | `=COUNTIF(Applications!Q:Q,"Under Review")` |
| Applications – Interview | `=COUNTIF(Applications!Q:Q,"Interview")` |
| Applications – Offer | `=COUNTIF(Applications!Q:Q,"Offer")` |
| Applications – Rejected | `=COUNTIF(Applications!Q:Q,"Rejected")` |
| Applications – Withdrawn | `=COUNTIF(Applications!Q:Q,"Withdrawn")` |
| Applications – No Response | `=COUNTIF(Applications!Q:Q,"No Response")` |
| Applications – Total | `=COUNTA(Applications!D:D)-1` |

## Settings tab (A2:C9)

| Setting | Value | What it is |
|---|---|---|
| profile_doc | {link to the profile doc you created} | Your Candidate Profile Google Doc |
| resume_doc | {link to the resume doc you created} | Your resume as plain text |
| cover_letter_folder | {link to the Cover Letters folder} | Where cover-letter drafts are saved |
| timezone | {user's IANA timezone, e.g. America/Toronto} | Used for dates |
| min_fit_score | 6 | Only add leads with this fit score or higher (1–10) |
| cover_letter_min_fit | 7 | Draft a cover letter for leads at or above this score |
| max_new_postings_per_run | 15 | How many new postings an agent opens per run (lower = cheaper runs) |
| use_gmail_alerts | {yes if Gmail is connected and the user agreed, else no} | yes = also read LinkedIn/Seek job-alert emails (read-only) |

## Dropdowns (data validation, not strict)

- Job Leads, column P (Lead Status), rows 2–5000: New, Shortlisted, Applied, Skipped, Expired
- Applications, column Q (Status), rows 2–5000: Applied, Under Review, Interview, Offer, Rejected, Withdrawn, No Response
- Watchlist, column C (priority), rows 2–2000: A, B, X

## Start Here text (column A, rows 1–6)

1. Job Search Tracker  (bold, size 14)
2. Created by the job-search-agent skill. Don't rename tabs or reorder columns – the skills write to them by position.
3. Job Leads: set Lead Status (column P) and Your Skip Reason (column V). The agent learns from those.
4. Markets: one row per country you search in. Settings: links and limits.
5. Watchlist (optional): employers you like. Priority A = scanned every run, B = rotated, X = never.
6. To search: "Run the job search for {country}". To apply: "Start my application assistant".

## Markets rows – starting points by country

Fill one row per target country. If the user needs no sponsorship there, write "Citizen / no sponsorship needed"
(or "Permanent resident / no sponsorship needed") in the route column. If they do, use the route below and add
"(check official government sources – rules change)" to Notes. Search keywords come from the user's target roles.

| Country | Route if sponsorship is needed | Job boards |
|---|---|---|
| Canada | Employer-supported work permit: LMIA, or LMIA-exempt routes such as the Global Talent Stream | Job Bank, LinkedIn alerts, company careers pages, Greenhouse/Lever boards |
| United States | Employer-sponsored work visa (e.g. H-1B; others depend on nationality) | LinkedIn alerts, company careers pages, Greenhouse/Lever/Ashby boards |
| United Kingdom | Skilled Worker visa through a licensed sponsor (Home Office register of licensed sponsors) | LinkedIn alerts, company careers pages |
| Germany | EU Blue Card; prefer English-language roles | StepStone, Arbeitnow, LinkedIn alerts, company careers pages |
| Netherlands | Highly skilled migrant through a recognised sponsor (IND public register) | LinkedIn alerts, company careers pages |
| Ireland | Critical Skills Employment Permit or General Employment Permit | LinkedIn alerts, company careers pages |
| Australia | Employer-sponsored visa (e.g. Skills in Demand, subclass 482) through an approved sponsor | Seek AU (alerts by email, from:seek.com.au), LinkedIn alerts |
| New Zealand | Accredited Employer Work Visa (employer must be accredited by Immigration NZ) | Seek NZ (alerts by email, from:seek.co.nz), LinkedIn alerts |
| Other | Write "Check official government sources" and ask the user what they know | LinkedIn alerts, company careers pages |
