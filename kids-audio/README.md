# Kids' Audiobook Chooser

A weighted ranking tool for ~220 audiobooks suited to listeners ages 8–12. Adjust sliders to prioritize what matters — age fit, length, engagement, and recency — and the table re-ranks in real time.

## Features

- **Weighted ranking** across four dimensions with instant re-ranking
- **Filterable columns** for genre, engagement, series, and Libby availability
- **Search** by title or author
- **Libby integration** — check audiobook availability at Berkeley Public Library via OverDrive's API
- **Hoopla links** — search for audiobooks on Hoopla Digital

## Dataset

221 audiobooks spanning fantasy, realistic fiction, historical fiction, adventure, mystery, humor, sci-fi, and animal stories. Curated for middle-grade listeners (ages 8–12), from classics (Charlotte's Web, Narnia) to recent favorites (Wings of Fire, Nevermoor).

## How it works

Everything runs client-side in a single HTML file with no build step. Book data is loaded from `books.csv` via PapaParse. The only external call is the optional Libby availability check, which hits OverDrive's Thunder API.

## Built with

Claude Code (Anthropic) — both the code and the dataset.
