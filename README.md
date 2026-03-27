# Book Chooser

Built entirely by Claude Code (Anthropic) — both the code and the dataset.

A tool for finding your next read from ~1,100 works of literary fiction, filtering on key characteristics.

- **Readability** — how easy the book is to read (1 = easiest, 10 = hardest)
- **Length** — page count (fewer = better)
- **Recency** — year published (more recent = better)
- **Canon tier** — how canonical the book is (1 = undisputed peak, 9 = lowest)
- **Conventionality** — how traditionally narrated (1 = radically experimental, 10 = straightforward storytelling)

Adjust the sliders to change how much each dimension matters. The table re-sorts in real time. You can also search by title or author, filter by column, and sort by any column.

## Data

**Note: all data is currently from Claude and unchecked. There are likely errors.**

`books.csv` contains ~1,100 works of literary fiction with columns for title, author, year published, canon tier, primary type, tone, scope, readability, conventionality, pages, and language. The app parses whatever columns exist dynamically — adding new columns won't break anything.

### Where the list came from

The initial ~340 books were generated from Claude's training knowledge, drawing on standard canon lists and critical consensus. That seed list was then expanded to ~1,000 by cross-referencing several PDF source lists:

- Harold Bloom's Western Canon appendix
- The Library 100: Top 500 Novels
- NYT 100 Best Books of the 21st Century
- The Greatest Books Since 2000
- Our Users' Top 100 (The Greatest Books)
- Books That Everyone Should Read At Least Once (Goodreads, multiple pages)
- The Great American Read checklist (TGAR 2018)
- A "New Literary Fiction" recommendations list

Books from these sources were filtered to literary fiction only (no genre fiction, children's books, or non-fiction), deduplicated, and categorized.

An additional ~150 books from 2023–2025 were added by searching prize lists and critics' year-end lists:

**Prize lists:** Booker Prize longlists/shortlists/winners (2023–2025), International Booker Prize longlists (2023–2024), National Book Award longlists (2023–2024), Women's Prize for Fiction longlist (2023), Pulitzer Prize fiction finalists (2024–2025), PEN/Faulkner finalists (2023), Center for Fiction First Novel Prize (2023), National Book Critics Circle longlist (2024), Kirkus Prize winners.

**Critics' year-end and best-of lists:** NYT 100 Notable Books + Top 10 (2023–2025), New Yorker Best Books (2024–2025), Guardian Best Fiction (2024–2025), Kirkus Best Fiction (2023–2025), Publishers Weekly Best Fiction (2024), Literary Hub Ultimate Best of + Most Anticipated + 43 Favorites (2023–2025), Electric Literature Best Novels (2025), Time 100 Must-Reads (2024), NPR Books We Love (2023–2024), Vulture Best Books (2025), Book Marks Best Reviewed (2023), Library Journal Best Literary Fiction (2023–2024).

A final pass added ~40 books to fill systematic gaps (mid-century American women writers, short story masters, Indian literature in translation, African fiction beyond the canonical names, and several underrepresented British novelists like Muriel Spark, Barbara Pym, Penelope Fitzgerald, and Anita Brookner).

The starting framework for the type taxonomy came from a fiction taxonomy document generated in Claude Web.

### Why recent years are overrepresented

The list deliberately includes more books per year for recent decades than for earlier ones:

- Pre-1900 literature is represented by the established canon — the books that have survived critical reassessment over a century or more. A handful per decade.
- The 20th century gets broader coverage, roughly scaling up as you approach the present, because more books remain in print and in critical conversation.
- 2023–2025 have ~15 books each — roughly the same rate as 2020–2021 — after pruning the most speculative entries (tier 9 and weaker tier 8) to avoid recency bias in the dataset.
- The tier system handles the quality signal — a tier 8 book from 2024 is explicitly marked as "possible" canon, not proven.

All metadata — canon tier, primary type, tone, scope, readability, page count, and original language — was assigned by Claude based on critical consensus and knowledge of each book. Canon tiers 1–7 reflect relative critical standing; tiers 8–9 are recent books too new to assess. Readability (1–5) measures prose difficulty, not emotional difficulty or plot complexity. About a third of the primary type assignments were hand-verified; the rest were assigned heuristically.

### Primary types

Each book is tagged with a dominant reading experience: Psychological Portrait, Social World, Moral Crucible, Interiority, Dreamlike, Compressed, Epic/Generational, Satirical, Formal/Experimental, or Fable/Allegory.

## How matching works

Each book gets a match score based on a weighted average of five dimensions (any slider set to 0 disables that dimension). Books missing a value are scored on the remaining dimensions. The match column shows a visual bar — fuller means a stronger match for your current slider settings.

**Length** and **recency** use log-linear scaling to capture diminishing returns:

- **Length**: Log scale from 150 to 900 pages. Books ≤150 pages get the best score; ≥900 pages get the worst. The difference between 150 and 300 pages matters much more than 700 vs 850.
- **Recency**: Log scale on distance from 2022. Recent books (2020 vs 1990) are differentiated much more than older ones (1750 vs 1720). Anything before 1700 gets the same worst score.

**Readability** (1–10), **canon tier** (1–9), and **conventionality** (1–10) use simple linear min-max normalization across the dataset.

## Setup

Hosted on GitHub Pages. To run locally, serve the directory over HTTP:

```
cd book-chooser
python3 -m http.server 8000
```

Then open http://localhost:8000. Opening `index.html` directly won't work because browsers block local file fetches.

## Tech

Single `index.html` file. No framework, no build step. Uses [PapaParse](https://www.papaparse.com/) from CDN to load the CSV at runtime.
