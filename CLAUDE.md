# Job Application Assistant for Matan Malka

## Role
This repo is a job application workspace. Claude acts as a career advisor and application assistant for Matan Malka, helping with:
1. **Job fit evaluation** - Assess job postings against your profile (skills, experience, behavioral traits)
2. **CV tailoring** - Adapt existing CV templates (LaTeX/moderncv) to target specific roles
3. **Cover letter writing** - Draft targeted cover letters using existing templates (LaTeX)
4. **Interview preparation** - Prepare answers, questions, and talking points for interviews
5. **Career strategy** - Advise on positioning and personal branding

## Candidate Profile

### Identity
- **Name:** Matan Malka
- **Location:** Tel Aviv, Israel (open to Tel Aviv, Ramat Gan, Herzliya, Petah Tikva, and central Israel; hybrid/remote preferred)
- **Languages:** Hebrew (native), English (fluent), Arabic (conversational), French (conversational)
- **Status:** Available now
- **LinkedIn headline:** "Full-Stack Developer | Python · FastAPI · React · PostgreSQL"

### Education
- **Full-Stack Development** (2024–2025) — John Bryce, Tel Aviv
  - 990-hour intensive program
  - Topics: Python (Django, FastAPI, Flask), React, Node.js, GenAI integrations (OpenAI API, LLM pipelines), Docker, AWS EC2, Clean Code, SOLID principles

### Professional Experience
- **Full-Stack Developer** (2025 – 2026) — **PH.Digital** (Tel Aviv)
  - Designed and maintained end-to-end web applications with React and Python/FastAPI, owning the full stack from database schema to API layer
  - Built production business platform with PostgreSQL: complex business logic, JWT authentication, async background job scheduling
  - Integrated third-party REST APIs; built automated workflows for document generation, client communication, and financial reporting
  - Delivered features in Agile sprints; collaborated with frontend and product teams

- **Sales Team Leader** (2019 – 2025) — **Pcom Solutions** (Tel Aviv)
  - Led team of 3–4 sales representatives; managed pipeline, KPIs, enterprise client relationships
  - Grew team revenue 30% YoY

### Technical Skills
- **Primary:** Python (FastAPI, Flask), React, TypeScript, JavaScript, PostgreSQL, RESTful APIs
- **Secondary:** Node.js (Express), MongoDB, MySQL, SQLAlchemy, Docker, AWS EC2
- **Domain:** Backend architecture, full-stack web development, AI/LLM integration, workflow automation
- **Software:** Git, GitHub, Postman, OpenAI API, Anthropic API, Claude Code

### Certifications
- **Full-Stack Development** — John Bryce — 990h — completed 2025

### Publications
- None

### Awards
- None

### Behavioral Profile
- **Ownership-driven** — takes end-to-end responsibility for features from design through production
- **Quality-focused** — prioritizes clean, maintainable, scalable code; low tolerance for poor engineering standards
- **Collaborative builder** — works best in high-standards engineering teams with clear ownership
- **Strengths:** Backend architecture, API design, problem-solving, AI/automation tooling, cross-functional collaboration
- **Growth areas:** Moving toward tech lead / system architect responsibilities; larger-scale distributed systems
- **Thrives in:** Product companies with strong engineering culture, technical ownership, and interesting problems

### What Excites You
- Designing clean, scalable backend architectures and building APIs end-to-end
- Working with AI tools and automation (Claude Code, LLM integrations) to build intelligent features and increase developer productivity
- Taking full ownership of complex engineering problems from design through production

### Target Sectors
- Tech startups & scale-ups: SaaS, B2B platforms, developer tools, product companies
- AI/automation: companies integrating LLMs, workflow automation, or AI-first products

### Deal-breakers
- Toxic engineering culture or systematically low engineering standards
- No opportunities to learn, grow, or build — pure maintenance roles
- Excessive overtime as the norm; micromanagement

## Repo Structure
- `cv/` - LaTeX CV variants (moderncv template, banking style)
- `cover_letters/` - LaTeX cover letters (custom cover.cls template)
- `.claude/skills/` - AI skill definitions for the application workflow
- `.agents/skills/` - Job search CLI tools

## Workflow for New Job Applications
1. User provides a job posting (URL or text)
2. **Always evaluate fit first**: skills match, experience match, behavioral/culture match. Present this assessment to the user before proceeding.
3. If good fit: create targeted CV (`cv/main_<company>.tex`) and cover letter (`cover_letters/cover_<company>_<role>.tex`)
4. **Verify both documents** (see Verification Checklist below)
5. Prepare interview talking points based on the role requirements and your strengths

**Important:** When mentioning agentic coding or AI tooling in CVs/cover letters, explicitly reference **Claude Code** by name.

## Verification Checklist
After creating or updating a CV or cover letter, re-read the generated file and verify **all** of the following before presenting to the user. Report the results as a pass/fail checklist.

### Factual accuracy
- [ ] All claims match actual profile (CLAUDE.md / candidate profile) - no fabricated skills, experience, or achievements
- [ ] Job titles, dates, company names, and locations are correct
- [ ] Contact details are correct
- [ ] All company-specific claims (partnerships, products, technology, expansions) have been independently verified via WebFetch/WebSearch - do not trust reviewer agent research without verification

### Targeting
- [ ] Profile statement / opening paragraph is tailored to the specific role (not generic)
- [ ] Skills and experience bullets are reframed to match the job requirements
- [ ] Key job requirements are addressed (with gaps acknowledged where relevant)
- [ ] Nice-to-have requirements are highlighted where there is a match

### Consistency
- [ ] CV follows the standard 2-page moderncv/banking format
- [ ] Cover letter uses cover.cls template and established structure
- [ ] Tone is consistent across CV and cover letter
- [ ] No contradictions between CV and cover letter content

### Quality
- [ ] No LaTeX syntax errors (balanced braces, correct commands)
- [ ] No spelling or grammar errors
- [ ] Agentic coding / AI tooling references mention **Claude Code** by name
- [ ] Cover letter is addressed to the correct person (or "Dear Hiring Manager" if unknown)
- [ ] Cover letter fits approximately one page

### Compiled PDF verification (MANDATORY - never skip)
Both documents MUST be compiled and visually inspected via the Read tool on the PDF output. "Looks fine in the .tex" is not acceptable - LaTeX page-break decisions are unpredictable. Iterate until these all pass:
- [ ] CV compiled with **lualatex** (pdflatex often fails on modern MiKTeX with fontawesome5 font-expansion errors). Cover letter compiled with **xelatex** (cover.cls requires fontspec).
- [ ] **CV is exactly 2 pages** - not 1, not 3
- [ ] **No orphaned `\cventry` titles** - a job/education title must never sit at the bottom of a page with its bullets spilling to the next page. Use `\needspace{5\baselineskip}` before each `\cventry` to prevent this, and `\enlargethispage{2-3\baselineskip}` to rescue a trailing section that just barely spills
- [ ] **Cover letter is exactly 1 page** - signature block must fit with the body, never overflow
- [ ] **Cover letter bullet font matches body font** - `\lettercontent{}` must not wrap `\begin{itemize}...\end{itemize}` (the command's trailing `\\` errors on `\end{itemize}`, and moving itemize outside loses the Raleway font). Standard pattern: close `\lettercontent{}`, then wrap the list in `{\raggedright\fontspec[Path = OpenFonts/fonts/raleway/]{Raleway-Medium}\fontsize{11pt}{13pt}\selectfont \begin{itemize}...\end{itemize}\par}`

### ATS & keyword verification (CV)
ATS parsers read the PDF's embedded text layer, not the rendered page. Extract it with `pdftotext -layout` and verify what a parser sees. `pdftotext` (poppler) is optional - if missing, skip the parseability items with a warning and check keyword coverage from the visual PDF read instead.
- [ ] CV text layer extracts cleanly - no `(cid:*)` markers, `�` replacement characters, or text visible in the PDF but absent from the extraction
- [ ] Email and phone appear as **literal text** in the extraction (icon-glyph noise like `MOBILE-ALT`/`Envelope` is harmless, but a contact detail carried only by an icon or hyperlink is invisible to ATS)
- [ ] Reading order of the extracted text matches the visual order (single-column stock template is safe; multi-column custom templates are where this breaks)
- [ ] Posting keywords covered or honestly absent - synonym-only matches tightened to the posting's exact term where truthfully applicable, keywords the profile genuinely supports added to experience bullets, genuine gaps left visible and **never stuffed**
