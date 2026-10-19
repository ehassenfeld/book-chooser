# YA Book Chooser

A prototype of 100 books for an advanced middle-school reader: 75 young adult award books and 25 grown-up books a strong 12-year-old can handle. Same idea as the main book chooser: adjust the sliders and the table re-ranks.

## Where the books come from

The YA books are all on at least one of these lists. The award results come from each award's own published list (ALA, the National Book Foundation, Mystery Writers of America, CILIP), not from memory.

- Michael L. Printz Award, winners and honors (2000–2026)
- National Book Award for Young People's Literature, winners and finalists (1996–2026)
- Edgar Award for Best Young Adult Mystery, winners and nominees (1989–2026)
- William C. Morris YA Debut Award, winners and finalists (2009–2026)
- Newbery Medal, winners and honors (1990–2026)
- Carnegie Medal, winners (2000–2026)
- Alex Awards, adult books with teen appeal (1998–2026)

The grown-up books are mostly classics middle schoolers read and like (Animal Farm, Agatha Christie, Fahrenheit 451), plus a few recent adult novels.

## What the columns mean

- **Acclaim** (1–5) comes from the awards. Winning the Printz, National Book Award, Newbery or Carnegie is 5. A Printz honor, National Book Award finalist, Newbery honor, Edgar winner or Morris winner is 4. An Edgar nominee, Morris finalist or Alex Award is 3. Appearing on two different lists adds one. Classics with no award were scored by hand.
- **Pull** (1–5) is how hard the book is to put down. Claude's judgment.
- **Maturity** (1–3): 1 is fine at 12, 2 is a parental call, 3 is for older teens. Hover over it for what drives the score. Where Common Sense Media has rated the book (76 of 100), the score follows its age rating: 12 and under is a 1, 13–14 is a 2, 15 and up is a 3. The other 24 are Claude's estimates, and the hover says so.
- **Descriptions** are Claude's, checked against publisher summaries.

## Read marks

A check mark means the book has been read. "Hide read" clears those out of the way. The marks come from the `read` column in `books.csv`, which is updated by hand.

## Tech

Single `index.html`, data in `books.csv`, PapaParse from a CDN. The Libby button checks ebook availability at Berkeley Public Library through OverDrive's public catalog API. To run locally, serve the parent folder over HTTP (`python3 -m http.server 8000`) and open `/ya/`.

Built by Claude Code (Anthropic).
