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

**Methods and Analysis**: Comparative text analysis across two temporal corpora, including VADER and TextBlob sentiment analysis, TF-IDF feature extraction, agency/blame attribution scoring, and BERTopic modeling with NER for entity-level framing analysis.

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
│   ├── raw/                                # Raw source-level files
│   │   ├── GDELT/                          # GDELT GKG mention CSVs
│   │   │   ├── gdelt_20190701_20190704_cloudflare_mentions.csv
│   │   │   ├── gdelt_20211207_20211210_aws_mentions.csv
│   │   │   └── gdelt_20251117_20251120_cloudflare_mentions.csv
│   │   ├── Guardian/                       # Raw Guardian API exports
│   │   │   └── guardian_facebook_outage_2021-10_constraint.csv
│   │   ├── NYT/                            # Raw NYT API exports
│   │   │   ├── NEW_nyt_cloudflare_20090101_20260202.csv
│   │   │   └── nyt_facebook_outage_2021-10-04.csv
│   │   └── postmortem_all.csv              # Scraped post-mortem reports
│   │
│   ├── pre_AI/                             # Curated Pre-AI event datasets (2019–2021)
│   │   ├── guardian_aws_2021.csv
│   │   ├── guardian_facebook_outage_2021-10.csv
│   │   ├── guardian_fastly_2021.csv
│   │   ├── guardian_google_2020.csv
│   │   ├── nyt_aws_2021.csv
│   │   ├── nyt_cloudflare_2019-07-02.csv
│   │   ├── nyt_facebook_outage_2021-10-04.csv
│   │   ├── nyt_facebook_outage_2021-10.csv
│   │   ├── nyt_fastly_2021.csv
│   │   └── nyt_google_2020.csv
│   │
│   ├── post_AI/                            # Curated Post-AI event datasets (2024–2025)
│   │   ├── guardian_aws_2025.csv
│   │   ├── guardian_azure_2025.csv
│   │   ├── guardian_cloudflare_outage_2025-11-17_2025-1-20.csv
│   │   ├── guardian_crowdstrike_2024.csv
│   │   ├── guardian_google_cloud_2025.csv
│   │   ├── nyt_aws_2025.csv
│   │   ├── nyt_azure_2025.csv
│   │   ├── nyt_cloudflare_2025-11-18.csv
│   │   ├── nyt_crowdstrike_2024.csv
│   │   ├── nyt_google_cloud_2025.csv
│   │   └── postmortem_all.csv
│   │
│   ├── merged_all_articles.csv             # Combined article-level table across events & sources
│   ├── merged_guardian_fulltext.csv         # Guardian-focused merged full-text table
│   ├── merged_relevant_articles.csv        # Filtered corpus for downstream analysis
│   │
│   └── analysis&visualization/             # Cleaned analysis outputs & generated figures
│       ├── agency_intensity_results_clean.csv
│       ├── agency_prevalence_results_clean.csv
│       ├── guardian_analyzed_clean.csv
│       ├── keyword_frequency_results_clean.csv
│       ├── tfidf_results_clean.csv
│       ├── fig_agency_by_event_clean.png
│       ├── fig_agency_heatmap_clean.png
│       ├── fig_keyword_frequency_clean.png
│       ├── fig_sentiment_by_event.png
│       ├── fig_sentiment_distributions.png
│       └── fig_tfidf_distinctive_words_clean.png
│
├── scripts/
│   ├── News_Data_Collection1.ipynb         # Data collection: APIs, downloads, post-mortem scraping
│   ├── data_cleaning.ipynb                 # Cleaning, harmonization, dataset preparation
│   ├── visualization&analysis.ipynb        # Sentiment, TF-IDF, agency analysis, plotting
│   └── BertTopic_pre_postAI_comparison.ipynb  # BERTopic modeling & NER-based era comparison
│
├── progress_report_1.md                    # Check-in 1: scope, data status, team plan
├── progress_report_2.md                    # Check-in 2: progress update
└── README.md
```

- `data/raw/` — unprocessed API exports, GDELT downloads, and scraped post-mortem reports
- `data/pre_AI/` & `data/post_AI/` — curated per-event datasets split by era
- `data/analysis&visualization/` — cleaned analysis CSVs and all generated figures
- `scripts/` — Jupyter notebooks for collection, cleaning, analysis, and BERTopic modeling

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
| transformers | (BERTopic/NER) |
| bertopic | (BERTopic modeling) |

Standard library modules: `os`, `re`, `json`, `math`, `time`, `datetime`, `pathlib`, `warnings` (bundled with Python 3.13.5).

---

# Contributions

- **Zhimeng (Brittany) An**: Led and completed all data collection workflows — NYT API, Guardian API, GDELT downloads, and post-mortem web scraping (Cloudflare, Meta, AWS). Organized the raw data directory structure and maintained repository organization. Primary author of `News_Data_Collection1.ipynb`.
- **Zehan Li**: Completed all data cleaning, harmonization, visualization, and analysis — including TF-IDF comparative analysis, VADER/TextBlob sentiment analysis, agency/blame attribution scoring, and all figure generation. Primary author of `data_cleaning.ipynb` and `visualization&analysis.ipynb`.
- **Simmons Yin**: Conducted additional analysis using BERTopic modeling and Named Entity Recognition (NER) for entity-level framing comparison across eras. Primary author of `BertTopic_pre_postAI_comparison.ipynb`.

---

# AI Usage Statement

- **ChatGPT (OpenAI)**: Used for debugging code errors, brainstorming analysis approaches, and refining notebook documentation.

---

# Project Links

- **Slides used in the in-class presentation**: [link]
- **Updated final slides (full version)**: [link]
- **Presentation video**: [link]
