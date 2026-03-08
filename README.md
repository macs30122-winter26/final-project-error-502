# Catastrophic Backtracking

---

# Project Description

## Summary

This project examines how media narratives describe major digital infrastructure failures before and after the AI boom — a gap we call the **"interpretive lag"** between technical reality and public/media framing.

- **Topic**: Comparative analysis of news coverage surrounding large-scale tech outages across two eras — Pre-AI (2019–2021) and Post-AI (2024–2025)
- **Research Questions**:
  - How does news vocabulary differ between Pre-AI and Post-AI outage coverage?
  - Do sentiment polarity and emotional intensity differ across eras?
  - Which actors (companies, systems, users, or AI) are framed as responsible or agentive in each era?
  - How closely does public/news framing match technical post-mortem explanations?
- **Why it matters**: As AI increasingly permeates public discourse, understanding whether and how it reshapes the framing of unrelated technical failures reveals broader shifts in media sense-making and public attribution of technological responsibility

## Additional Info

**Total lines of code**: ~2,500 lines (across collection, cleaning, analysis, and visualization notebooks)

**Methods and Analysis**: Comparative text analysis across two temporal corpora, including VADER and TextBlob sentiment analysis, TF-IDF feature extraction, agency/blame attribution scoring, and BERT-based NER for entity-level framing analysis.

**Project strength**: Analysis and visualizations — the project produces a rich set of comparative figures (sentiment distributions, TF-IDF keyword contrasts, agency heatmaps) that clearly illustrate framing shifts across eras.

---

# Data

| Source | Retrieval Link | Collection Method | Notes |
|--------|---------------|-------------------|-------|
| New York Times (Archive API + Article Search API) | [developer.nytimes.com/apis](https://developer.nytimes.com/apis) | API | Outage-related articles filtered by event keywords |
| The Guardian (Content Search API) | [open-platform.theguardian.com](https://open-platform.theguardian.com/documentation/) | API | Full-text access via Open Platform |
| GDELT Global Knowledge Graph (GKG) | [data.gdeltproject.org/gkg](https://data.gdeltproject.org/gkg/index.html) | Direct CSV download | Event-level records, locally processed |
| Official engineering post-mortems (Cloudflare, Meta, AWS) | [blog.cloudflare.com](https://blog.cloudflare.com/), [engineering.fb.com](https://engineering.fb.com/), [aws.amazon.com/message/12721](https://aws.amazon.com/message/12721/) | Web scraping | Incident reports used as technical ground truth |

---

# Repository Structure

```
final-project-error-502/
├── data/
│   ├── raw/                            # Raw source-level files (API exports, downloads)
│   │   ├── nyt/
│   │   ├── guardian/
│   │   ├── gdelt/
│   │   └── postmortem/
│   ├── pre_AI/                         # Curated Pre-AI event datasets
│   ├── post_AI/                        # Curated Post-AI event datasets
│   ├── merged_all_articles.csv         # Combined article-level table across events & sources
│   ├── merged_guardian_fulltext.csv     # Guardian-focused merged full-text table
│   ├── merged_relevant_articles.csv    # Filtered corpus for downstream analysis
│   └── analysis&visualization/         # Cleaned analysis outputs & generated figures
│       ├── tfidf_results_clean.csv
│       ├── agency_*_clean.csv
│       └── *.png
│
├── scripts/
│   ├── News_Data_Collection1.ipynb     # Data collection: APIs, downloads, post-mortem scraping
│   ├── data_cleaning.ipynb             # Cleaning, harmonization, dataset preparation
│   └── visualization&analysis.ipynb    # Sentiment, TF-IDF, agency analysis, plotting
│
├── docs/
│   └── progress_report_1.md            # Progress report: scope updates, data status, team plan
│
└── README.md
```

- `data/` — raw downloads, curated era-specific subsets, merged corpora, and analysis outputs/figures
- `scripts/` — Jupyter notebooks for collection, cleaning, and analysis
- `docs/` — project documentation and progress reports

---

# Libraries

| Library | Version |
|---------|---------|
| Python | 3.13.5 |
| JupyterLab | 4.3.4 |
| notebook | 7.3.2 |
| pandas | 2.2.3 |
| numpy | 2.1.3 |
| matplotlib | 3.10.0 |
| seaborn | 0.13.2 |
| scipy | 1.15.3 |
| scikit-learn | 1.6.1 |
| vaderSentiment | 3.3.2 |
| textblob | 0.19.0 |
| requests | 2.32.3 |
| beautifulsoup4 | 4.12.3 |
| transformers | (BERT/NER) |

Standard library modules: `os`, `re`, `json`, `math`, `time`, `datetime`, `pathlib`, `warnings` (bundled with Python 3.13.5).

---

# Contributions

- **Zhimeng (Brittany) An**: Led and completed all data collection workflows — NYT API, Guardian API, GDELT downloads, and post-mortem web scraping (Cloudflare, Meta, AWS). Organized the raw data directory structure and maintained repository organization. Primary author of `News_Data_Collection1.ipynb`.
- **Zehan Li**: Completed all data cleaning, harmonization, visualization, and analysis — including TF-IDF comparative analysis, VADER/TextBlob sentiment analysis, agency/blame attribution scoring, and all figure generation. Primary author of `data_cleaning.ipynb` and `visualization&analysis.ipynb`.
- **Simmons Yin**: Conducted additional analysis using BERT-based models and Named Entity Recognition (NER) for entity-level framing, and contributed to statistical comparison across eras.

---

# AI Usage Statement

- **ChatGPT (OpenAI)**: Used for debugging code errors, brainstorming analysis approaches, and refining notebook documentation.
- **Claude (Anthropic)**: Used for drafting and editing written components (progress reports, README), code review, and exploring analytical framing strategies.

Each team member is responsible for verifying the accuracy and originality of all AI-assisted outputs.

---

# Project Links

- **Slides used in the in-class presentation**: [link]
- **Updated final slides (full version)**: [link]
- **Presentation video**: [link]
