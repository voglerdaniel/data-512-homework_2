# Getting Quality Predictions for World Politicians' Wikipedia Articles

### Homework #2 – Data 512
### Daniel Vogler

## Introduction

The purpose of this project is to collect and analyze a set of data about the quality of English-language Wikipedia articles about politicians around the world. I request basic information about the individual pages from the Wikimedia Page Info API, then request information about article quality from the ORES API. These sources are combined with population data to compute and analyze metrics of **articles per capita** and **high-quality articles per capita**.

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

8 directories, 23 files; intermediate_data_batches folder is omitted for brevity.

```

## Research Implications

Before s
