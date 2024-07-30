# CWRCzech

CWRCzech (**C**lick **W**eb **R**anking dataset for **Czech**) is a 100M query-document Czech click dataset for relevance ranking with user behavior data derived from the search engine logs of Seznam.cz. It contains over 2.7 million distinct queries and over 8.4 million documents. It contains queries in Czech that were identified by the search engine as an informational intent (e.g., “how to boil an egg”).  

When constructing the dataset, our goal was to avoid sensitive information, user identification, and harmful content. To this end, we adhered to the following protocol: All queries classified as porn or obscene were filtered; as well as bot queries. To prevent an accidental leak of numerical information, only queries with alphabetical characters were selected. Finally, each query had a minimal occurrence in 5 unique requests within the specified time frame (i.e., the same query was requested by at least 5 users) to ensure anonymization and to prevent potential identification of
specific users or their sensitive information. 

The dataset was introduced in paper [CWRCzech: 100M Query-Document Czech Click Dataset and Its Application to Web Relevance Ranking](https://arxiv.org/pdf/2405.20994) which has been accepted at the SIGIR 2024.

## Obtaining the Annotated Data
Please, first read a [disclaimer](./disclaimer.md) that contains the terms of use. If you comply with them, send an email to srch.vyzkum@firma.seznam.cz and the link to the dataset will be sent to you.


## Overview 

The dataset contains the following columns:
- requestId: Id of the particular request with a single query.
- query: User query with corrected typos and added diacritical marks.
- url: Document URL.
- title: Words from the document classified by the search engine as a title.
- bte: Body text extract, i.e., document body snippet processed by the internal search engine model and trimmed to 230 characters. It is empty for the webpages that block search engines or prohibit usage of their contents for GPT training.
- rank: Position of the document in the search results page. Indices may be absent in cases where a document was no longer indexed at the time of dataset creation.
- clicks: The number of clicks on a given document in given search results.
- dwellTime: Time in seconds spent in the clicked document page before the user returned to the search results page. This information is not always available, typically for the last click in the search results.

The files are distributed as parquet files – to load the dataset in pandas, use
```
import pandas as pd
df = pd.read_parquet(path)
```

## Acknowledgements

If you find our work helpful, please consider citing us:

```
@inproceedings{vonasek2024cwrczech,
  title={CWRCzech: 100M Query-Document Czech Click Dataset and Its Application to Web Relevance Ranking},
  author={Von{\'a}sek, Josef and Straka, Milan and Kr{\v{c}}, Rostislav and Lasonov{\'a}, Lenka and Egorova, Ekaterina and Strakov{\'a}, Jana and N{\'a}plava, Jakub},
  booktitle={Proceedings of the 47th International ACM SIGIR Conference on Research and Development in Information Retrieval},
  pages={1221--1231},
  year={2024}
}
```
