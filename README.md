# Catastrophic Backtracking

## Project Description

This project examines how media narratives describe major digital infrastructure failures before and after the AI boom. We call this gap between technical reality and public/media framing the "interpretive lag." Our corpus compares Pre-AI outage events (e.g., 2019-2021) and Post-AI outage events (e.g., 2024-2025), then measures how language, tone, and responsibility framing change across periods.

Research questions:

- How does news vocabulary differ between Pre-AI and Post-AI outage coverage?
- Do sentiment polarity and emotional intensity differ across eras?
- Which actors (companies, systems, users, or AI) are framed as responsible or agentive in each era?
- How closely does public/news framing match technical post-mortem explanations?

Current workflow in this repository:

- Collect outage-related reporting from multiple sources.
- Clean and merge event-level corpora.
- Run comparative text analysis (sentiment, keyword frequency, TF-IDF, agency metrics).
- Generate cleaned outputs and figures for progress reports and final write-up.

## Data

- New York Times APIs (Archive API + Article Search API). Retrieval link: [https://developer.nytimes.com/apis](https://developer.nytimes.com/apis). Collection method: API.
- The Guardian Open Platform (Content Search API). Retrieval link: [https://open-platform.theguardian.com/documentation/](https://open-platform.theguardian.com/documentation/). Collection method: API.
- GDELT Global Knowledge Graph (GKG). Retrieval link: [https://data.gdeltproject.org/gkg/index.html](https://data.gdeltproject.org/gkg/index.html). Collection method: direct download of CSV files, then local processing.
- Official engineering post-mortems and incident reports (Cloudflare, Meta, AWS). Retrieval links: [https://blog.cloudflare.com/](https://blog.cloudflare.com/), [https://engineering.fb.com/](https://engineering.fb.com/), [https://aws.amazon.com/message/12721/](https://aws.amazon.com/message/12721/). Collection method: web scraping.

## Libraries

- Python `3.13.5`
- JupyterLab `4.3.4`
- notebook `7.3.2`
- pandas `2.2.3`
- numpy `2.1.3`
- matplotlib `3.10.0`
- seaborn `0.13.2`
- scipy `1.15.3`
- scikit-learn `1.6.1`
- vaderSentiment `3.3.2`
- textblob `0.19.0`
- requests `2.32.3`
- beautifulsoup4 `4.12.3`
- Python standard library modules used in notebooks (`os`, `re`, `json`, `math`, `time`, `datetime`, `pathlib`, `warnings`) come with Python `3.13.5`.

## Repo Structure

- `data/raw/`: raw source-level files, including API exports and downloaded files (NYT, Guardian, GDELT, postmortem raw files).
- `data/pre_AI/`: curated Pre-AI event datasets.
- `data/post_AI/`: curated Post-AI event datasets.
- `data/merged_all_articles.csv`: combined article-level table across events and sources.
- `data/merged_guardian_fulltext.csv`: Guardian-focused merged full-text table.
- `data/merged_relevant_articles.csv`: filtered merged corpus used for downstream analysis.
- `data/analysis&visualization/`: cleaned analysis outputs and generated figures (`tfidf_results_clean.csv`, `agency_*_clean.csv`, and plots).
- `scripts/News_Data_Collection1.ipynb`: collection notebook for APIs, downloads, and post-mortem scraping.
- `scripts/data_cleaning.ipynb`: cleaning, harmonization, and dataset preparation.
- `scripts/visualization&analysis.ipynb`: sentiment, keyword, TF-IDF, agency analysis, and plotting.
- `progress_report_1.md`: progress documentation for scope updates, data status, and team plan.

## Contributions

- Zhimeng (Brittany) An: built and maintained collection workflows (NYT, Guardian, GDELT, and post-mortem scraping), and led Cloudflare event data collection, handled repository organization.

- Zehan Li: collected and organized the 2021 Facebook outage case, and produced comparative visualizations, led cleaning and analysis pipeline work (TF-IDF, sentiment, agency, and statistical comparison).

- Simmons Yin: collected and organized the 2021 AWS outage case, doing the statiscal comparison.

