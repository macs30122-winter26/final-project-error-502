# Progress Report 1 — Error-502

**Team Members:** Zehan Li, Simmons Yin, Zhimeng (Brittany) An

---

## Project Update

Our project investigates the "interpretive lag" between technical reality and public perception during major digital infrastructure failures. We compare how news media and public discourse frame failures in the **Pre-AI era** versus the **AI era**, analyzing differences in sentiment, agency, and vocabulary.

**Changes from original proposal:** We have made two notable adjustments. First, we have **expanded the Pre-AI case study** beyond the single 2019 Cloudflare outage. Because major mainstream outlets (NYT, Guardian) published very few articles specifically about the 2019 Cloudflare event, we added two additional Pre-AI events: the **2021 Facebook/Instagram/WhatsApp global outage (Oct 4, 2021)** and the **2021 AWS S4 outage (Dec 07, 2021)**. Both occurred before ChatGPT's launch (Nov 2022) and generated substantial global coverage — our initial collection confirms strong data availability (Facebook outage — NYT: 15 direct + 82 related articles, Guardian: 80 direct + 400+ related; AWS outage — GDELT: 312 articles), effectively resolving the Pre-AI data scarcity problem. Second, we have **broadened our news sources** beyond the originally proposed NYT and Guardian APIs to include GDELT GKG data and Fox News, ensuring wider coverage across both mainstream and non-mainstream outlets. Our core research questions and focus area (Option 4: Textual Data Analysis) remain unchanged.

---

## Data Status

- **New York Times API** — [https://developer.nytimes.com/apis](https://developer.nytimes.com/apis)
  - ✅ Collected. Cloudflare events: event-window queries for 2019 and 2025 (1 article each); all Cloudflare-related articles 2009–present (~10 relevant after filtering from 122). **2021 Facebook outage: 15 articles directly addressing the event, 82 articles mentioning related content.**
  - Included in original proposal.
  - Issue: Very limited Cloudflare-specific coverage; resolved by adding the 2021 Facebook outage as a second Pre-AI case, which yields substantially more data.

- **The Guardian API** — [https://open-platform.theguardian.com/documentation/](https://open-platform.theguardian.com/documentation/)
  - ✅ Collected. Cloudflare events: 0 results for 2019 event window, 2 articles for 2025; all Cloudflare-related articles (~9 total). **2021 Facebook outage: 80 articles directly addressing the event, 400+ articles mentioning related content.**
  - Included in original proposal.
  - Issue: No Cloudflare 2019 event-window coverage; resolved by the 2021 Facebook outage, which provides extensive Pre-AI data from this source.

- **GDELT Global Knowledge Graph (direct download)** — [https://data.gdeltproject.org/gkg/index.html](https://data.gdeltproject.org/gkg/index.html)
  - ✅ Collected. Downloaded daily GKG CSV files for event windows (t−1 to t+2). Cloudflare events: 38 articles (2019), 620 articles (2025). **2021 AWS S4 outage: 312 articles collected.** Sources are predominantly non-mainstream outlets.
  - New source (not in original proposal). Added to broaden coverage beyond major outlets.
  - Issue: Noisy data requiring further cleaning and deduplication.


- **Reddit API (via PRAW)** — [https://www.reddit.com/dev/api/](https://www.reddit.com/dev/api/)
  - 🔄 In progress. API access application submitted and awaiting approval. Once approved, we will target r/technology, r/sysadmin, r/ChatGPT for event-window discussions.
  - Included in original proposal.

- **Official Engineering Post-Mortems (web scraping)** — Cloudflare Blog & OpenAI Status
  - 🔄 In progress. Code being developed to scrape official incident reports as "technical ground truth."
  - Included in original proposal.

**Summary of data balance:** Post-AI (2025) data is abundant (~620+ GDELT articles, plus NYT/Guardian/Fox coverage). Pre-AI data has been substantially strengthened by adding two additional events: the 2021 Facebook outage (NYT: 15 direct + 82 related; Guardian: 80 direct + 400+ related) and the 2021 AWS outage (GDELT: 312 articles). Combined with the original 2019 Cloudflare data (~40–50 articles across sources), the Pre-AI corpus is now comparably sized, addressing our earlier data imbalance concern.

---

## Analysis Plan Update

Our focus area remains **Option 4: Textual Data Analysis**. The planned analyses are:

1. **Text preprocessing pipeline:** Tokenization, stop-word removal, and lemmatization using NLTK/spaCy across all collected corpora.
2. **TF-IDF analysis:** Identify distinguishing vocabulary between Pre-AI and AI-era discourse — testing whether Pre-AI text uses more mechanistic language ("CPU spike," "configuration," "bug") while AI-era text uses more anthropomorphic/opaque language ("hallucination," "confusion," "unpredictable").
3. **Sentiment analysis (VADER):** Compare emotional intensity and polarity across eras, with time-series plots over the event windows.
4. **N-gram frequency analysis:** Map collocations and phrase patterns that characterize each era's framing.
5. **Embedding-based semantic similarity (exploratory):** Use text embeddings to measure semantic distance between public discourse and official engineering post-mortems — quantifying the "interpretive gap" between technical reality and public perception.
6. **Exploratory statistical comparison:** Descriptive statistics and at least one method from class (e.g., t-test comparing mean sentiment scores across eras).
7. **Visualizations:** Word clouds, comparative bar charts (TF-IDF top terms), time-series sentiment plots, and n-gram frequency plots using Matplotlib/Seaborn.

No major changes from the original plan. The addition of embedding-based semantic similarity is an extension that complements our original TF-IDF approach by capturing meaning beyond keyword overlap.

---

## Timeline

| Week | Tasks |
|------|-------|
| **Week 5** (current) | Finalize and push all existing collection code and data. Complete progress report. Push incomplete Reddit scraping code. |
| **Week 6** | Expand Pre-AI data: collect 2021 Facebook outage data via GDELT, NYT, Guardian, Fox News APIs. Finish Reddit API scraping for all event windows. Complete engineering blog scraping. Link and deduplicate data across sources. |
| **Week 7** | Data cleaning and preprocessing (tokenization, normalization). Begin TF-IDF, sentiment analysis, and n-gram analysis. Produce initial visualizations. |
| **Week 7–8** | Progress Report 2. Review all analyses, refine visualizations, run exploratory stats. Begin embedding-based similarity analysis. |
| **Week 9** | In-class presentation. Finalize all figures and narrative. |
| **Week 10** | Final submission: polished code, README, video, updated presentation. |

---

## Team Responsibilities

| Member | Responsibilities |
|--------|-----------------|
| **Zhimeng (Brittany) An** | Data collection: writing and maintaining API/scraping scripts (NYT, Guardian, GDELT, Fox News, blog post-mortems). Led Cloudflare event data collection. |
| **Zehan Li** | Data collection for the 2021 Facebook outage case study. Visualization, conceptual framing, and project organization: designing comparative visualizations, maintaining GitHub repository structure, and shaping the research narrative. |
| **Simmons Yin** | Data collection for the 2021 AWS outage case study. Data processing and analysis: text cleaning pipeline, TF-IDF, VADER sentiment analysis, n-gram analysis, embedding-based semantic similarity, and exploratory statistics. |

**Changes from original proposal:** Zehan's role shifted from data acquisition to visualization and project organization; Brittany shifted from visualization to data collection. As the project expanded to multiple Pre-AI events, Zehan and Simmons each took ownership of collecting data for one additional case study (Facebook and AWS, respectively). Simmons's analysis role remains unchanged.
