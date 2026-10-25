# Topic Modelling of Financial Tweets

Do topics found by unsupervised topic modelling recover the categories that human annotators assigned to financial news tweets?

Project written in R.

## Data

The [`zeroshot/twitter-financial-news-topic`](https://huggingface.co/datasets/zeroshot/twitter-financial-news-topic) dataset: around 17,000 finance-related tweets, each manually annotated with one of 20 topic labels. The analysis uses a version with the labels written out as text (`text`, `manually_annotated_label`), and keeps six of them, for a subset of 4,790 tweets:

| Label | Tweets |
|---|---|
| Stock Commentary | 2,118 |
| General News \| Opinion | 1,557 |
| Personnel Change | 495 |
| Treasuries \| Corporate Debt | 321 |
| Analyst Update | 255 |
| IPO | 44 |

To run the analysis, place the CSV at `data/zeroshot_twitter_financial_news_topic_recoded.csv`.

## Methods

- **Pre-processing** (`quanteda`): corpus construction, tokenisation, removal of punctuation, URLs, numbers, symbols and English stop words, and a document-feature matrix with empty documents removed.
- **Topic modelling** (`topicmodels`): Latent Dirichlet Allocation with k = 6, matching the number of labels; topics interpreted from their top terms and a sample of tweets.
- **Comparison with human labels**: cross-tabulation of topics against the original labels.
- **Keyness analysis** (`quanteda.textstats`): words most distinctive of one topic relative to the rest, shown as a keyness plot and word clouds.
- **2D visualisation** (`quanteda.textmodels`, `plotly`): Latent Semantic Analysis projection of the tweets, coloured by topic.

## Findings

- The topics overlap only partly with the human labels. Some labels are concentrated in a few topics: 77% of *Stock Commentary* tweets fall into two topics, 74% of *Personnel Change* tweets into two others, and 55% of *Analyst Update* tweets into one. *General News | Opinion*, the second-largest label, is spread across all six topics.
- The category imbalance makes it hard for small labels such as IPO (44 tweets) to emerge as topics of their own.
- In the LSA projection, most tweets cluster closely together across topics; the main exception is a hashtag-heavy topic that spreads along the first dimension.

## Running the code

Open `analysis.Rmd` in RStudio and knit it. Required packages: `tidyverse`, `quanteda`, `quanteda.textplots`, `quanteda.textstats`, `quanteda.textmodels`, `topicmodels`, `plotly`.
