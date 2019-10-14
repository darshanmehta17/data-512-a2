# Bias in Data - <br> Analysis of Wikipedia Articles

> Authored by ***Darshan Mehta*** on *Oct 13, 2019*.

## Goal

The goal of this project is to understand the concept of bias in data by exploring Wikipedia — specifically, the articles on political figures from many countries. 

We will assess the quality of each of the articles using an online evaluation service and then study the quality of these articles across countries and regions with reference to their population.

The code and step-by-step walkthrough is present in [this Jupyter notebook](/hcds-a2-bias.ipynb).

## Data Sources

To perform the analysis, we will draw from two data sources:

- The Wikipedia articles dataset on politicians by country can be found on [Figshare](https://figshare.com/articles/Untitled_Item/5513449). This data has been extracted and is present in the file [page_data.csv](/page_data.csv).
- The population data is published by the Population Reference Bureau [here](https://www.prb.org/international/indicator/population/table). This dataset is present in the file [WPDS_2018_data.csv](/WPDS_2018_data.csv).

Furthermore, to get a quality score of the articles, we use the [Objective Revision Evaluation Service (ORES)](https://www.mediawiki.org/wiki/ORES). This service uses a machine learning system to predict the quality of an article present on the Wikipedia. We access this service using a library called as [oresapi](https://github.com/halfak/oresapi). 

This service rates the article into one of the following 6 categories:

| Rank | Symbol | Description |
|------|--------|-------------|
| 1 | FA | Featured Article |
| 2 | GA | Good Article |
| 3 | B | B-class Article |
| 4 | C | C-class Article |
| 5 | Start | Start-class Article |
| 6 | Stub | Stub-class Article |

For each article, the response would contains probability scores for each of the ranks along with a prediction which contains the symbol of the class which has the highest probability score. 

## Requirements
This analysis was prepared using Python 3.7 running in a Jupyter Notebook environment.  
- Documentation for Python can be found here: https://docs.python.org/3.7/
- Documentation for Jupyter Notebook can be found here: http://jupyter-notebook.readthedocs.io/en/latest/  

The following Python packages were used and their documentation can be found at the accompanying links:

- [pandas v0.23.4](https://pandas.pydata.org)
- [oresapi v0.0.1](https://github.com/halfak/oresapi)

## Generated Files
This notebook creates 2 CSV files of data extracted and compiled as part of this analysis.

- [wp_wpds_politicians_by_country.csv](/wp_wpds_politicians_by_country.csv): This is the final CSV generated as a result of the data preparation section present [here](/hcds-a2-bias.ipynb#Data-Preparation). The schema of this file is described below.

| Column | Description |
|--------|-------------|
| country | Name of the country |
| article_name | Name of the article |
| revision_id | Revision ID of the article on Wikipedia |
| article_quality | Quality class as determined by ORES |
| population | Population of the country |

- [wp_wpds_countries-no_match.csv](/wp_wpds_countries-no_match.csv): This file contains the details of articles from countries on which the population data was missing. The schema of this file is decribed below:

| Column | Description |
|--------|-------------|
| country | Name of the country |
| page | Name of the article |
| rev_id | Revision ID of the article on Wikipedia |
| article_quality | Quality class as determined by ORES |


## Generated Summaries
This notebook generates the following 6 summary tables in order to analyze the coverage and relative quality of the countries and the regions:

1. **Top 10 countries by coverage:** "10 highest-ranked countries in terms of number of politician articles as a proportion of country population".
2. **Bottom 10 countries by coverage:** "10 lowest-ranked countries in terms of number of politician articles as a proportion of country population".
3. **Top 10 countries by relative quality:** "10 highest-ranked countries in terms of the relative proportion of politician articles that are of GA and FA-quality".
4. **Bottom 10 countries by relative quality:** "10 lowest-ranked countries in terms of the relative proportion of politician articles that are of GA and FA-quality".
5. **Geographic regions by coverage:** "Ranking of geographic regions (in descending order) in terms of the total count of politician articles from countries in each region as a proportion of total regional population".
6. **Geographic regions by coverage:** "Ranking of geographic regions (in descending order) in terms of the relative proportion of politician articles from countries in each region that are of GA and FA-quality".

## License

This code is released under [MIT License](/LICENSE).

The license of the data sources can be found on the documentation page linked against each dataset in the [Data Sources](#data-sources) section.

The `oresapi` has released under MIT License which can be found [here](https://github.com/halfak/oresapi/blob/master/LICENSE).