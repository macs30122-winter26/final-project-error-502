# Progress Report 2 — Error-502

**Team Members:** Zehan Li, Simmons Yin, Zhimeng (Brittany) An

## Project Changes since Check 1

**Expanded event coverage from 3+3 to 5+5.** At Check 1 we had three Pre-AI events (Cloudflare 2019, Facebook 2021, AWS 2021) and three Post-AI events (CrowdStrike 2024, AWS 2025, Cloudflare 2025). The AWS 2021 event only had GDELT data and several events had very few articles. We added five new events and supplemented AWS 2021 with NYT/Guardian data, bringing the total to five Pre-AI (Cloudflare 2019, Google 2020, Fastly 2021, Facebook 2021, AWS 2021) and five Post-AI (CrowdStrike 2024, Google Cloud 2025, AWS 2025, Azure 2025, Cloudflare 2025). This improves event diversity so the analysis is not dominated by a single incident per era.

**Dropped GDELT from the analysis pipeline.** GDELT GKG data was collected for Cloudflare 2019, AWS 2021, and Cloudflare 2025, but the sources it indexes (blogs, trade press, local outlets) are too noisy and inconsistent for framing analysis. And considering the fact that GDELT data includes processed data without full text, our pipeline now uses only NYT and Guardian articles. GDELT data remains in the repository for reference and later potential comparison usage.

**Dropped Reddit and Fox News.** These were initially considered at Check 1 but proved impractical: Reddit lacks structured article text and API application was rejected, and Fox News has no public API. We decided to focus on the two-source design (NYT + Guardian)  for comparing mainstream media framing.

**Drafted data cleaning pipeline.** Built a standardized cleaning pipeline that: (1) unifies column names across Guardian and NYT (which have different schemas), concatenating NYT snippet + lead_paragraph as body_text since full article text is not available via the API; (2) standardizes dates to UTC, deduplicates by URL, removes empty titles; (3) creates analysis-ready fields including text_for_analysis, text_length, and has_full_text (>200 characters, distinguishing Guardian full-text from NYT snippets); (4) flags likely_relevant articles using outage-related keywords without auto-removing, allowing manual review; (5) outputs three CSVs — merged_all_articles.csv (complete), merged_relevant_articles.csv (filtered, used by analysis pipeline), and merged_guardian_fulltext.csv (Guardian only). Post-mortem reports are kept separate.

**Drafted  analysis pipeline.** Since Check 1, we built and ran the  analysis pipeline covering sentiment analysis (VADER + TextBlob), TF-IDF vocabulary comparison, keyword-based framing analysis, and agency/blame attribution analysis. 

**Collected five official post-mortem reports** from Cloudflare, Meta, CrowdStrike, and AWS engineering blogs. These are stored separately (postmortem_all.csv) and may be incorporated in future analysis.

### Analysis decisions based on EDA

After expanding to the 5+5 event set, we re-ran the full pipeline. Key findings:

**Sentiment analysis: no significant differences.** Both VADER (p=0.928) and TextBlob show no era-level sentiment shift on Guardian full-text. NYT title sentiment is also non-significant. We report this as a null result — outage coverage tone has not measurably changed between eras.

**Keyword framing: two significant shifts confirmed.**
1. AI/Tech Complexity framing increased from 15.0 to 23.1 per 1000 words (p<0.001). This result is robust across the expanded event set, supporting an "AI framing spillover" interpretation: even when outages are unrelated to AI, post-AI era reporting more frequently situates events within an AI/tech complexity narrative.
2. Infrastructure/System framing increased from 3.9 to 5.4 (p=0.014), a new finding with the expanded dataset.
3. Notably, Economic Impact — which was significant (p=0.006) in our earlier 3+3 analysis — is no longer significant (p=0.116) with 5+5 events. This suggests the earlier finding was partly driven by CrowdStrike's aviation disruption rather than a broad era-level trend.

**TF-IDF vocabulary reveals a broader narrative shift.** Post-AI distinctive words cluster around physical-world consequences (flights, airlines, cancelled, passengers, airport, cash), while pre-AI distinctive words center on digital/social contexts (social, media, content, users, account). This pattern — independent of our predefined keyword lists — suggests that infrastructure outages are increasingly framed in terms of real-world material disruption rather than digital inconvenience, reflecting how deeply technology infrastructure has become embedded in everyday life.

**Agency/blame attribution: no significant differences** at the era level, in either prevalence or intensity. By-event variation exists (e.g., CrowdStrike has the highest company_blame prevalence) but does not aggregate into a systematic era difference.

### Specific analysis decision based on EDA

Our initial 3+3 analysis showed Economic Impact framing was significant (p=0.006), but expanding to 5+5 events made it non-significant (p=0.116). This tells us the result was driven by CrowdStrike's aviation disruption rather than a genuine era-level shift. Based on this, we are making the following concrete decision: we will run **event-level Mann-Whitney U tests** on each framing category (AI/Tech Complexity, Infrastructure/System, Economic Impact, etc.) within each era, using event as the grouping variable. This will let us formally test whether within-era variation across events is larger than between-era variation — essentially a sensitivity check for confounding by event type. Variables: the dependent variable is keyword frequency per 1000 words (continuous), and the independent variable is era (binary: pre_ai / post_ai), with event as a stratification factor.

Additionally, we will combine Guardian and NYT data for the keyword framing and agency analyses. Both are normalized per 1000 words, making them comparable despite the text length difference. TF-IDF and sentiment will remain Guardian-only because TF-IDF requires comparable document lengths and sentiment scores saturate differently on long vs. short texts.

### Visualization improvements

Our current TF-IDF distinctive-words bar chart is dominated by event-specific terms (e.g., "airlines," "flights" for CrowdStrike; "social media," "twitter" for Facebook), making it hard to distinguish framing shifts from event composition effects. We will make two structural changes:

1. **Facet by event within each era**: instead of a single pre-AI vs. post-AI bar chart, create a faceted grid (one panel per event) so readers can see which TF-IDF terms are event-specific and which recur across multiple events within the same era.
2. **Add a framing keyword heatmap**: create a heatmap with events on the y-axis and the six framing categories on the x-axis, with color intensity representing keyword frequency per 1000 words. This will visualize both the era-level pattern and event-level variation in a single figure, replacing the current separate bar charts for each category.

### Focus area

Our focus area is **Option 4: Textual Data Analysis**. The core contribution is testing whether mainstream media framing of infrastructure outages shifted after the rise of generative AI — specifically whether coverage adopted more AI/technology complexity framing, stronger blame attribution, or different risk narratives. The methods central to this focus include: dictionary-based keyword frequency analysis with Mann-Whitney U tests, TF-IDF vocabulary extraction with custom stop-word filtering, VADER and TextBlob sentiment analysis, and regex-based agency/blame frame detection with Chi-squared and Mann-Whitney tests. All analyses compare pre-AI (before Nov 2022) vs. post-AI (after Nov 2022) era articles from the Guardian and NYT.

## Contributions

- **Zhimeng (Brittany) An**: Data collection — Cloudflare 2019, 2025 (NYT + Guardian), GDELT GKG (Cloudflare 2019, Cloudflare 2025), supplementary event collection script (Google 2020, Fastly 2021, AWS 2021, Google Cloud 2025, Azure 2025), post-mortem scraping; ongoing analysis refinement
- **Zehan Li**: Data collection — CrowdStrike 2024, AWS 2025, Cloudflare 2025; drafted data cleaning pipeline and analysis pipeline (sentiment, TF-IDF, framing keywords, agency attribution); ongoing analysis refinement
- **Simmons Yin**: Data collection — Facebook 2021 (NYT + Guardian), GDELT GKG (AWS 2021); ongoing analysis refinement
