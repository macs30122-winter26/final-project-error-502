# Error-502 Group Project

---

# Project Description

## Summary

This project examines how media narratives describe major digital infrastructure failures before and after the AI boom — a gap we call the **"interpretive lag"** between technical reality and public/media framing.

- **Topic**: Comparative analysis of news coverage surrounding large-scale tech outages across two eras — Pre-AI (2019–2021) and Post-AI (2024–2025)
- **Research Questions**:
  - Does the sentiment (tone) of outage coverage differ across eras?
  - What vocabulary and thematic frames distinguish pre-AI vs post-AI coverage?
  - Has the attribution of blame and agency — who/what gets held responsible — changed?
 
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
│   └── BertTopic_pre_postAI_comparison.ipynb  # BERTopic modeling preliminary exploring notes
│   └── extended_pipeline.ipynb     # BERTopic modeling & NER-based era comparison


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

- **Zhimeng (Brittany) An**: Led and completed all data collection workflows — NYT API, Guardian API, GDELT downloads, and post-mortem web scraping (Cloudflare, Meta, AWS). Organized the raw data directory structure and maintained repository organization. Conducted preliminary BERTopic explorations. Primary author of `News_Data_Collection1.ipynb` and `BertTopic_pre_postAI_comparison.ipynb`.
- **Zehan Li**: Completed all data cleaning, harmonization, visualization, and analysis — including TF-IDF comparative analysis, VADER/TextBlob sentiment analysis, agency/blame attribution scoring, and all figure generation. Primary author of `data_cleaning.ipynb` and `visualization&analysis.ipynb`.
- **Simmons Yin**: Conducted additional analysis using BERTopic modeling and Named Entity Recognition (NER) for entity-level framing comparison across eras. Primary author of `extended_pipeline.ipynb`.

---


# AI Usage Statement

**Tools used**: ChatGPT (OpenAI), Claude (Anthropic). All core logic, analysis design, and research decisions were made  by team members. AI was consulted  for  assistance as described below.

- **NYT API pagination, rate limiting, and UTC handling** (`News_Data_Collection1.ipynb`): Claude was consulted to debug the rate-limiting retry loop (HTTP 429 handling with time.sleep) when hitting the NYT Article Search API. Claude was additionally used to handle dates consistently UTC ISO format. Claude was also consulted to understand the nested JSON structure of NYT API responses 
- **Guardian full-text field extraction** (`News_Data_Collection1.ipynb`): Claude was consulted to understand the Guardian API's response JSON structure, including how to enable full article body text. Claude also helped verify the logic to implement a per-page time.sleep to stay within the Guardian API's rate limits during multi-page pagination
- **Regex pattern for date normalization** (`data_cleaning.ipynb`): ChatGPT was used to draft a regex pattern for parsing inconsistent date formats across sources.
- **Matplotlib subplot layout** (`visualization&analysis.ipynb`): ChatGPT was consulted to adjust subplot spacing and shared axis formatting for the sentiment distribution figure.
- **TF-IDF horizontal bar chart styling** (`visualization&analysis.ipynb`): ChatGPT was used to refine color mapping and label truncation for the distinctive-words figure.
- **BERTopic parameter selection** (`extended_pipeline.ipynb`): ChatGPT was consulted for guidance on `min_topic_size` and UMAP dimensionality parameters.


---

# Project Links

- **Slides used in the in-class presentation**: [https://docs.google.com/presentation/d/12K5dRpMGdQhw57jOoymh_BibeL8mv9z1/edit?slide=id.p3#slide=id.p3]
- **Updated final slides (full version)**: [https://docs.google.com/presentation/d/1nreu6XDMZ4hU5bWSnePgj0aaHqBmk5f6ecoDGYRqtAk/edit?slide=id.g3c4a32236bc_0_57#slide=id.g3c4a32236bc_0_57]
- **Presentation video**: [link]
