# Job Search Kit for Claude

An AI job-search assistant that runs inside **your own** Claude account. It finds new jobs that fit your resume in the
countries you choose, checks whether the employer can support your work rights, logs everything in a Google Sheet, and
drafts cover letters and LinkedIn notes. When you're ready to apply, a second assistant helps you fill the forms – you
review everything and click Submit yourself.

Your data stays in your own Google Drive and Claude account. Nothing is sent to the author of this kit.

*An independent, community project – not made by or affiliated with Anthropic. "Claude" is Anthropic's product.*

## What's inside

| File | What it is |
|---|---|
| `skills/job-search-agent/` | Sets everything up from a short chat, then finds and verifies new jobs for one country per run |
| `skills/apply-assistant/` | On-demand: updates application statuses from Gmail, removes duplicates, helps fill forms |
| `dist/` | The two skills as ready-to-upload zips |
| `templates/` | Blank tracker and profile template – only needed for manual setup |
| `examples/markets/` | Example rows for Canada, Germany, New Zealand, Australia, UK |

## What you need

- A Claude account. What each plan can do:

  | | Free | Paid (Pro, Max, Team, Enterprise) |
  |---|---|---|
  | Setup, manual searches, quick try, tailored resume, application status updates | ✅ | ✅ |
  | Filling application forms and live browser search (need Claude in Chrome) | ❌ | ✅ |
  | Automatic scheduled searches (e.g. twice a week, overnight) | ❌ | ✅ |
  | Room for full search runs | Limited – a run reads many pages and may hit Free limits | ✅ More room |

  On Free, start with **"quick job search"**, or lower `max_new_postings_per_run` in Settings (e.g. 5). The apply
  assistant still lists your new jobs without duplicates and gives you the links, cover letters and answers to paste.
  Plans and features change – check [Claude's help center](https://support.claude.com) for the current details.
- "Code execution and file creation" turned on in Claude **Settings → Capabilities** (skills need it).
- The **Google Drive** and **Google Sheets** connectors connected in Claude (**Gmail** optional).
- For filling forms and live browser search: the **Claude in Chrome** extension (paid plans), or the Claude desktop
  app's browser where available.

## Quick start (about 5 minutes)

1. Download `job-search-agent.zip` and `apply-assistant.zip` from the latest
   [release](https://github.com/sk9692-svg/job-search-kit/releases) (or the `dist/` folder).
2. In Claude go to **Customize → Skills**, click **+ → Create skill → Upload a skill**, upload each zip,
   and toggle both on. Connect Google Drive and Google Sheets.
3. In a new chat, say: **"Set up my job search"** and attach your resume.

Claude asks a few questions (roles, countries, whether you need sponsorship, deal-breakers), then creates a
**Job Search Kit** folder in your Google Drive with your tracker, your profile and a cover-letters folder.
Read the profile once and fix anything – it drives every search. Then:

- **"Run the job search for Canada"** – finds new jobs, scores them and drafts cover letters
- **"Start my application assistant"** – helps you apply; you click Submit
- **"Tailor my resume for lead 12"** – a version of your resume focused on that job, using only your real experience
- **"Search Naukri and Instahyre with my browser"** – a live search while you're online, for portals the normal search
  can't read (needs the Claude in Chrome extension or the Claude desktop app). It reads only the first couple of
  result pages, never signs in or applies, and stops if a site shows a CAPTCHA.

**Just want to try it?** Say **"quick job search"**. It searches one country and shows the best matches in the chat,
with no Google connection and nothing saved.

## Manual setup (optional)

Prefer to build the files yourself? About 30 minutes.

### 1. Tracker
1. Upload `templates/Job_Search_Tracker.xlsx` to Google Drive.
2. Open it → **File → Save as Google Sheets**. Name it exactly **Job Search Tracker** (the skills find it by name).
   Delete the uploaded .xlsx copy.

### 2. Your documents
1. Create a Google Doc, paste in `templates/candidate-profile-template.md`, and fill it in honestly.
2. Create a Google Doc with your resume as plain text.
3. Create a Drive folder for cover-letter drafts.
4. Paste the three links into the tracker's **Settings** tab.

### 3. Markets
Add one row per target country to the **Markets** tab (copy from `examples/markets/` and adjust keywords and cities).
Optionally add favourite employers to **Watchlist** (priority A = scanned every run).

### 4. Add the skills to Claude
1. Zip each skill folder on its own: `job-search-agent.zip` and `apply-assistant.zip`
   (the folder name inside the zip must match the skill name). Ready-made zips are in `dist/`.
2. In Claude go to **Customize → Skills**, click **+ → Create skill → Upload a skill**, upload each zip,
   and toggle both on.

### 5. Try it once in chat
- `Run the job-search agent for Canada` – check the leads it adds and the cover-letter drafts.
- `Start my application assistant` – it updates statuses and walks you through the new leads.

## Schedule the searches (optional)
Ask Claude to create a scheduled task, one per country, for example:

> Create a scheduled task that runs every Monday and Thursday at 7:00 am with this prompt:
> "Run the job-search-agent skill for Canada. My tracker is {link to your Job Search Tracker}."

If a scheduled run doesn't pick up the skill, paste the contents of `skills/job-search-agent/SKILL.md` into the
scheduled task's prompt instead, with the country and tracker link at the top.

**Keep usage down:** start with 2 runs a week per country, lower `max_new_postings_per_run` in Settings, and only add
countries you're serious about.

## How you work with it

- Agents add leads with Lead Status **New**. Set it to **Shortlisted** or **Skipped** (with a reason in
  "Your Skip Reason") – the agents learn from these and get better each run.
- Run the apply assistant whenever you have time to apply. It shows you what it will type, stops on the final review
  page, and only submits if you say yes for that job.
- You send LinkedIn notes yourself.
- Want a cover letter for every lead, not just strong matches? Set `cover_letter_min_fit` in Settings to a lower
  number (uses more of your Claude usage).
- Searching in India? Set up job alerts on Naukri, Instahyre, Cutshort, Hirist or Foundit and connect Gmail; the agent
  reads those alerts and checks each job on the employer's own site.

## Safety rules built in

- Never submits an application without your explicit yes for that job.
- Never types passwords, creates accounts, solves CAPTCHAs, or enters ID or bank numbers.
- Gmail is read-only: it never sends, replies, deletes or labels email.
- **Facts rule:** cover letters and forms use only what's in your resume and profile – no invented experience, and no
  claims about work rights you don't have.
- No auto-applying in bulk. Job sites' terms generally forbid it, and recruiters notice. This kit helps you send fewer,
  better applications.
- Avoids fee-charging "visa job" sites and scams.

## Limitations

- Many job portals (LinkedIn, Seek, Indeed, Naukri, Instahyre and others) can't be read by scheduled runs; those use
  your job-alert emails and the employer's own site. Live browser search reads some of them while you're online, but
  it's deliberately limited – portals don't allow bulk automated collection, and heavy use can get accounts restricted.
- Visa and work-permit rules change. The examples are starting points, not immigration advice – check official
  government sources.
- AI can make mistakes. Review every lead and every draft before you use it.

## Stop or remove it

- **Pause searches:** pause or delete the scheduled tasks in Claude.
- **Remove the skills:** Claude → Customize → Skills → turn them off or delete them.
- **Delete your data:** delete the **Job Search Kit** folder in Google Drive (tracker, profile, resume copy, cover
  letters). Nothing else is stored by the kit.
- **Disconnect Google:** remove the Google connectors in Claude's settings if you no longer need them.

## Changelog

- **v0.2** – One-sentence setup ("Set up my job search"), quick-try mode without Google, India job boards via alerts,
  tailored resume per job (real facts only), live browser search for portals like Naukri and Instahyre, Free vs paid
  guide.
- **v0.1** – First release: search agent, apply assistant, tracker template, profile template.

## Problems or ideas?

Open an [issue on GitHub](https://github.com/sk9692-svg/job-search-kit/issues): what you asked Claude, what happened,
and what you expected. Please remove personal details (resume text, emails, phone numbers) before posting.

## License

MIT – see `LICENSE`. Use it, change it, share it.
