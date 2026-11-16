# Application Basics Autofill

A reusable AI agent skill for the factual sections of university applications: read original records, interpret form fields, fill and verify saved drafts, and consolidate missing information into focused questions.

**This package contains a template for applicants to enter their own information and a skill that guides the agent's work.** The repository contains only general instructions and blank templates, with no built-in applicant profile, data collection code or telemetry code.

## Capabilities

- Fill personal details, education and academic records, tests, employment, projects, activities, honours and all non-essay factual short answers.
- Upload existing attachments, including completed SOP, PS and other essay files, after checking the intended applicant, programme, version and upload requirements.
- Identify conflicting dates, GPA definitions and resume versions without guessing; continue independent sections when one field lacks evidence.
- Create or reuse a private folder for each school and maintain one progress Markdown in place, reusing an existing equivalent record so work can resume without duplicate files.
- Leave essay writing and revision for separate work. Follow the authorization for each recommender invitation, payment or declaration, provided the action does not also submit the application.

**The agent never submits an application, even with explicit authorization.** It prepares and verifies drafts and attachments; the applicant performs final review and submission. Combined actions such as “Pay and submit” also belong to the applicant.

Form filling uses the current environment's existing browser connection and document-reading tools. Each institution's portal requires page-by-page interpretation; automated operation is not guaranteed on every website.

## User guide

### 1. Connect your browser

**Recommended: install OpenAI's ChatGPT browser extension**, including the Microsoft Edge version if you use Edge. Use the installation links provided by the desktop app or the [official browser extension setup guide](https://learn.chatgpt.com/docs/chrome-extension).

In an up-to-date ChatGPT desktop app, open **Settings > Computer Use**, select your browser (under **More browsers** if needed), and follow the plugin and extension installation prompts. Return to the settings and confirm that the browser shows **Manage**. Start a ChatGPT Work or Codex chat and select the browser or application tab with an `@`-mention. Use the browser profile where you installed the extension. Availability depends on rollout and workspace settings; see the [official guide](https://learn.chatgpt.com/docs/chrome-extension) for current requirements.

This skill assumes that a working browser connection is already available. It contains instructions and templates, not a browser automation engine. The host agent also needs permission and tools to read your designated local documents and upload files. Installing the extension alone does not install this skill or grant access to your files.

### 2. Install the skill

Copy the entire `skills/application-basics-autofill/` directory into the skills directory supported by your agent. For Codex, use the user-level `$CODEX_HOME/skills/` directory, typically `~/.codex/skills/` when the environment variable is unset. For other hosts, follow their skill installation instructions.

Keep `SKILL.md`, `agents/`, `assets/` and `references/` together. Confirm that your agent can find `application-basics-autofill` before starting an application.

### 3. Fill your private information template

If you do not already have an equivalent profile, copy the [blank applicant profile and material index](skills/application-basics-autofill/assets/private-workspace-template.md) once as `Applicant_Profile.md` to a **private directory outside the repository**. Edit this private copy in a text or Markdown editor. Reuse it across schools; never enter personal information into the public repository's template.

- **Personal details:** enter your own name and the contact information required by the application. Add the source location or confirmation date in the adjacent column.
- **Education and tests:** add a row for each relevant institution and test, with dates and paths to transcripts, certificates or score reports. Preserve the official wording; the agent checks GPA and other details against the originals.
- **Employment, projects, activities and honours:** record factual roles, dates and contributions, with references to your resume or supporting records. Leave uncertain details blank or mark them `Needs confirmation`.
- **Recommenders:** complete this section only when needed. Providing contact details does not authorize an invitation.
- **Private workspace locations and material index:** identify your application root and the existing files the agent should read. Include each file's path or accessible private reference, version or issue date, and intended use. List completed SOP/PS files here if you want them uploaded. Keep original files in their existing locations.

You do not need to fill every cell before starting. A blank value means unknown, not `No` or `Not applicable`. For sensitive identity fields, prefer a reference to the original document instead of copying the number into the profile. Never include passwords, verification codes, session cookies or access tokens. The agent must reopen the relevant originals; the profile is an index and starting point, not a substitute for evidence.

### 4. Start an application

Open the school's application portal in the connected browser, sign in yourself, and identify the correct tab. Tell the agent the school, programme, intake, private profile location and any existing school folder or progress Markdown. Specify which attachment versions are ready for this application, including a completed SOP/PS when applicable. Resolve login, verification-code or CAPTCHA prompts yourself if the portal requires them.

Replace the bracketed placeholders in this example before sending it:

> Use $application-basics-autofill for [school, programme, intake] in [the selected browser tab or portal URL]. My private profile is [path to Applicant_Profile.md]; use its references to reopen my original materials. Reuse [existing school folder and progress Markdown], or create a school folder with one Application.md if none exists. Complete all non-essay factual fields and short answers. Upload [the designated attachment paths and versions], including my completed SOP if listed. Save and verify the draft, group missing-information questions together, and update the same progress Markdown. Do not write or revise essays. Never submit the application.

The agent checks the records, fills supported answers, handles newly revealed fields, uploads the designated existing files and verifies saved results. If evidence is missing or conflicting, it asks you rather than guessing. Check its questions and supply corrections or additional original records as needed.

### 5. Resume and review

To continue later, point the agent to the same private profile, school folder, progress Markdown and application tab:

> Resume this application with $application-basics-autofill. Read [the existing school progress Markdown], check the current portal state, and continue the unfinished factual sections and designated uploads. Update the same file without creating another progress record. Never submit the application.

Review every answer, attachment preview and unresolved item in the portal yourself. **Only you perform final submission.** The agent must also stop before any combined action that submits, such as payment, declaration or upload buttons that finalize the application.

Workflow: install the skill → fill your private template and identify original records and completed attachments → specify the application page in the connected browser and the task scope → the agent verifies the records, fills factual answers, uploads the designated files and checks the saved draft → the applicant reviews and submits personally.

## Minimal private workspace

```text
Private_Applications/
  Applicant_Profile.md
  School_Name/
    Application.md
```

These are defaults for new records, not required renames. Reuse existing school folders and progress Markdown files even when named differently. Each school has one active progress Markdown for all programmes and intakes, separated by headings. It also holds material-location notes, so no extra school README is needed.

The agent updates that same file after a section or at handoff, recording section-level save status, attachment paths and versions, unresolved questions, and the next step. It does not create dated progress copies, detailed field ledgers or separate reports. Existing source documents and completed essays stay where they are and are referenced by path. Screenshots, spreadsheets, PDFs, logs and backup files are not generated by default.

Normally, a new school adds only one folder and one progress Markdown; an existing school reuses both. The shared profile is created only if needed, and school progress is not duplicated in it. Existing historical records are preserved rather than deleted to impose this layout. Final submission always remains the applicant's responsibility.

## Privacy boundaries

Do not include transcripts, resumes, identity documents, home addresses, recommender contact details, application IDs, chat exports, browser sessions or secrets in repository files, issues, pull requests or public screenshots. Use a minimal example with entirely fictional information when reporting a problem.

This skill includes no network upload script, but the host model and tools may process the materials you provide, and the application portal receives the information entered into it. The skill does not guarantee that data stays on your computer. `.gitignore` can reduce accidental inclusion; it cannot remove information from existing Git history.

## Publishing and contributing

Before publishing, review every file's contents and name, confirm that templates remain blank, and inspect Git commit authors, email addresses and history. Do not initialize a personal application directory as a public repository; publish only this separate template directory. A public GitHub repository displays its owner's account.

This version does not include an automated privacy scanner. Neither `.gitignore` nor a single keyword check guarantees that personal information will not be disclosed. Contributed examples must be entirely fictional; changing the name on a real applicant's background does not make it an anonymous example.

## Scope summary

An evidence-first skill for factual university application sections, all non-essay factual short answers and uploads of existing attachments, including completed SOP/PS files. It reopens original records, maps fields by meaning, handles conflicts without guessing, verifies saved drafts, and keeps applicant data in a separate private workspace. It does not write or revise essays and never submits applications. Payment and recommender messages require their own authorization and must not submit the application. Browser/document capabilities come from the host agent.

MIT licensed. The repository contains no real applicant examples.
