# Getting Quality Predictions for World Politicians' Wikipedia Articles

### Homework #2 – Data 512
### Daniel Vogler

## Introduction

The purpose of this project is to collect and analyze a set of data about the quality of English-language Wikipedia articles about politicians around the world. I request basic information about the individual pages from the Wikimedia Page Info API, then request information about article quality from the [ORES API](https://www.mediawiki.org/wiki/ORES). These sources are combined with population data to compute and analyze metrics of **articles per capita** and **high-quality articles per capita**.

## Repository Stucture

This repository has the following structure (created using the [tree command](https://stackoverflow.com/questions/2444402/how-do-i-display-a-tree-of-things-in-bash) in `bash`.):

```
.
├── LICENSE
├── cleaned_data
│   ├── article_revisions.json
│   ├── duplicated_politicians.csv
│   ├── politicians_by_country_AUG_2024_clean.csv
│   └── population_by_country_AUG_2024_clean.csv
├── code
│   ├── analysis.ipynb
│   ├── apikeys
│   │   ├── KeyManager.py
│   │   ├── KeyManager_BriefUserGuide.pdf
│   │   ├── __init__.py
│   │   └── __pycache__
│   │       ├── KeyManager.cpython-312.pyc
│   │       └── __init__.cpython-312.pyc
│   ├── dataset_combination.ipynb
│   ├── getting_article_quality_predictions.ipynb
│   └── resolving_data_inconsistencies.ipynb
├── directory_structure.txt
├── output_data
│   ├── adjusted_regional_populations.csv
│   ├── data_for_analysis.csv
│   ├── quality_predictions.json
│   └── wp-countries_no-match.txt
├── raw_data
│   ├── politicians_by_country_AUG.2024.csv
│   └── population_by_country_AUG.2024.csv
└── resources
    ├── wp_ores_liftwing_example.ipynb
    └── wp_page_info_example.ipynb

8 directories, 23 files; intermediate_data_batches folder and README file are omitted for brevity.

```

### Data Folders

This repository has four data folders:
- `raw_data`: the original, completely unmodified data specifying *which* politicians to pull information about
- `cleaned_data`: the raw data, transformed to [resolve inconsistencies](.//code/resolving_data_inconsistencies.ipynb)
- `intermediate_data_batches`: batches of article prediction quality data; these can be stitched together to form the complete dataset recording article quality
- `output_data`: the major, processed datasets contributing to the final analysis. Only basic computations are executed on these data in the [analysis notebook](.//code/analysis.ipynb); otherwise they are unmodified.


## Research Implications

Before starting to work with this data (see `raw_data` [folder](./raw_data/)), I expected politicians from large, wealthy countries, especially English-speaking ones, to be over-represented in this dataset relative to their countries. This would reflect the high profiles of politicians from these countries on the world stage and the fact that their countries predominantly speak English. I was surprised to find that several large countries (Netherlands, US, Mexico, Canada, United Kingdom, etc.) are [not represented](./output_data/wp-countries_no-match.txt) in the dataset. It is possible that they were omitted from the politicians dataset as outliers, but this is impossible to test since they are not included. In the course of my data processing and analysis, I found that the sources of bias I anticipated may have still played a role, even if the countries I expected to drive this effect weren't present. Northern Europe and the Caribbean, two regions with significant English fluency (even if it is often spoken as a second langauge) and close ties to English-speaking countries had some of the highest rates of high-quality articles per 1M inhabitants; East Asia and South Asia had some of the lowest rates. To validate my hypothesis about biases, future researchers should supplement this dataset by including politicians from countries that were omitted and add current politicians from countries that are already in the dataset[^1]. They could also supplement this analysis by joining the dataset I produced with a dataset of English-speaking rates by country to investigate whether countries with many English speakers are indeed over-represented relative to population.

As I reflect on what I learned from this project, a few things stand out. 

Firstly, this is a reminder that the way metrics are constructed is extremely influential. Researchers need to deeply understand the limitations of constructed metrics and exercise healthy skepticism about conclusions driven by them. For example, in this analysis South Asia and East Asia have an extremely low number of high-quality articles about politicians per capita. Is this evidence of bias against South Asia and East Asia on English Wikipedia? Maybe not. Although India has roughly 5x the population of the United States, its [houses of parliament](https://en.wikipedia.org/wiki/Parliament_of_India) have a comparable number of representatives to those of the United States. Arguably, the pool of possible politicians (taking legislators as a rough proxy) is a more appropriate denominator than total country population, since, as this example demonstrates, the number of politicians in a country and its population are not necessarily proportional.

Secondly, this project reinforced the importance of adopting good practices when working with large datasets. The calls to the ORES API took several hours to complete; I was very grateful that I took a batched approach (see `code/getting_article_quality_predictions.ipynb`) when I discovered a bug that would have required me to re-run everything. Instead, I was able to piece together the batches I had saved. 

[^1]: For example, Shinzo Abe and Olaf Scholz do not appear in the raw data, even though other politicians from Japan and Germany do. 
