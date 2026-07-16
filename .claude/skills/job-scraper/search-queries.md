# Search Queries for Job Scraper — Matan Malka (Israel / Tel Aviv)

## Installed portal CLIs (primary for `/scrape`)

`/scrape` auto-discovers portal skills under `.agents/skills/*/SKILL.md`. Active CLIs:
- **`linkedin-search`** — LinkedIn public job listings, country-agnostic. Primary CLI. Use `-l "Tel Aviv, Israel"` or `-l "Israel"`.
- **`freehire-search`** — freehire.dev tech aggregator. Use `--country IL` or `--city "Tel Aviv"`.

The `site:` queries below are **WebSearch fallbacks** — for portals without a CLI or when CLIs fail.

## Search Sites (WebSearch fallback)

Primary Israeli job boards:
- **drushim.co.il** — largest Israeli general job board
- **alljobs.co.il** — major Israeli job board
- **jobmaster.co.il** — major Israeli job board, strong tech coverage

Secondary (company career pages via Google):
- Direct `site:<company>.com/careers` for known target companies

## Query Categories

### Priority 1: Full-Stack Developer (strongest direction)

LinkedIn CLI:
```
bun run src/cli.ts search -q "full stack developer" -l "Tel Aviv, Israel" --jobage 14 --format table
bun run src/cli.ts search -q "full stack developer python" -l "Israel" --jobage 7 --format table
bun run src/cli.ts search -q "full stack engineer" -l "Tel Aviv, Israel" --jobage 14 --remote hybrid --format table
```

freehire CLI:
```
bun run src/cli.ts search -q "full stack" --country IL --category fullstack --format table
bun run src/cli.ts search -q "react fastapi" --country IL --format table
```

WebSearch fallback:
```
site:drushim.co.il "Full Stack Developer" "Python" OR "FastAPI" OR "React"
site:alljobs.co.il "Full Stack Developer" "Python" OR "React"
site:jobmaster.co.il "Full Stack Engineer" "Python" OR "TypeScript"
```

### Priority 2: Backend / Python Developer

LinkedIn CLI:
```
bun run src/cli.ts search -q "python backend developer" -l "Tel Aviv, Israel" --jobage 14 --format table
bun run src/cli.ts search -q "backend engineer python fastapi" -l "Israel" --jobage 14 --format table
bun run src/cli.ts search -q "node.js backend developer" -l "Tel Aviv, Israel" --jobage 14 --format table
bun run src/cli.ts search -q "python developer" -l "Tel Aviv, Israel" --remote hybrid --format table
```

freehire CLI:
```
bun run src/cli.ts search --category backend --skill python --country IL --format table
bun run src/cli.ts search -q "python fastapi postgresql" --country IL --format table
bun run src/cli.ts search --category backend --skill node.js --country IL --format table
```

WebSearch fallback:
```
site:drushim.co.il "Backend Developer" "Python" OR "FastAPI"
site:alljobs.co.il "Python Developer" Tel Aviv
site:jobmaster.co.il "Backend Engineer" "Python" OR "FastAPI" OR "Node.js"
```

### Priority 3: Software Engineer / AI-Augmented (adjacent roles)

LinkedIn CLI:
```
bun run src/cli.ts search -q "software engineer python react" -l "Tel Aviv, Israel" --jobage 14 --format table
bun run src/cli.ts search -q "software engineer" -l "Tel Aviv, Israel" --jobage 7 --remote hybrid --format table
bun run src/cli.ts search -q "software engineer llm ai" -l "Israel" --jobage 14 --format table
```

freehire CLI:
```
bun run src/cli.ts search -q "software engineer" --country IL --seniority junior,middle --format table
bun run src/cli.ts search --category fullstack,backend --country IL --remote hybrid --format table
```

WebSearch fallback:
```
site:drushim.co.il "Software Engineer" "Python" OR "React" Tel Aviv
site:alljobs.co.il "Software Developer" "Full Stack" OR "Python"
```

### Priority 4: TypeScript / Node.js / JavaScript (wide net)

LinkedIn CLI:
```
bun run src/cli.ts search -q "typescript developer" -l "Tel Aviv, Israel" --jobage 14 --format table
bun run src/cli.ts search -q "react developer" -l "Israel" --jobage 7 --format table
bun run src/cli.ts search -q "node.js developer" -l "Tel Aviv, Israel" --jobage 14 --format table
```

freehire CLI:
```
bun run src/cli.ts search --skill typescript,react --country IL --format table
```

WebSearch fallback:
```
site:drushim.co.il "TypeScript Developer" OR "Node.js Developer" Tel Aviv
site:alljobs.co.il "JavaScript Developer" "React" OR "Node.js" Tel Aviv
```

## Location Filter

Verify job location is within reasonable commute from Tel Aviv:
- **Ideal:** Tel Aviv, Ramat Gan, Givatayim, Petah Tikva
- **Acceptable:** Herzliya, Bnei Brak, Holon, Bat Yam, Rishon LeZion
- **Borderline:** Netanya, Rehovot (~45–60 min by transit) — flag for user
- **Too far:** Jerusalem, Haifa, Be'er Sheva — flag for review, likely skip
- **Remote / hybrid:** Always PASS

## Date Filter

Only include jobs posted within the last 14 days, or with an active deadline. Flag "date unknown" if posting date cannot be determined.

## Adapting Queries

If the user specifies a focus area (e.g. `/scrape python`), run Priority 2 queries first plus 2-3 custom queries for that focus. For `/scrape remote`, add `--remote remote` to all CLI calls and filter WebSearch results for "remote" or "עבודה מהבית".
