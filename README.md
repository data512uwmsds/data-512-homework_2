# Considering Bias in Data

## Introduction
This project explores bias in data, focusing on Wikipedia articles about political figures from various countries. The goal is to analyze how the coverage and quality of these articles vary across nations and geographic regions. Using a combination of datasets—one containing Wikipedia articles on politicians and another on country populations—we estimate article quality with the help of the machine learning service ORES (Objective Revision Evaluation Service). The analysis identifies potential gaps or biases in Wikipedia’s coverage of politicians and their article quality based on regions and population.

## License
This project is licensed under the MIT License. See the `LICENSE` file for details.

### Wikimedia Data
The dataset created in this project is based on the data from Wikimedia, sourced through the Wikimedia Info API. The Objective Revision Evaluation Service (ORES), used in this project to predict Wikipedia article quality scores, is a service provided by the Wikimedia Foundation. 

All data provided by the Wikimedia Foundation is available under the Creative Commons Attribution-ShareAlike 4.0 International License (CC BY-SA 4.0) and GNU Free Documentation License (GFDL) licenses. All the data sourced through the Wikimedia REST API is licensed under the CC-BY-SA 3.0 and GFDL licenses.

The Wikimedia Foundation's terms of use can be found [here](https://foundation.wikimedia.org/wiki/Policy:Terms_of_Use).

### Data Sources
Licenses of data sources in `raw` folder.

The dataset `politicians_by_country.AUG.2024.csv` was generated by crawling the Wikipedia category “Politicians by nationality”. Wikipedia content is available under the Creative Commons Attribution-ShareAlike 3.0 Unported License (CC BY-SA 3.0).

The dataset `population_by_country_AUG.2024.csv` was downloaded from the [World Population Data Sheet](https://www.prb.org/international/indicator/population/table) published by the [Population Reference Bureau](https://www.prb.org/). This data is subject to the Population Reference Bureau's usage policies.

### Included Code Samples
The code sample provided in this repository for making API requests to Wiki Info and ORES is licensed under the [CC-BY 4.0 License](https://creativecommons.org/licenses/by/4.0/) and included in the `sample_notebook` folder. 

## Output Data Files

**Datasets** <a name="output-data-files"></a>
Several output data files are generated for the analysis. These are stored in `data` folder.

1. `wp_politicians_by_country.csv`
This is the file that merges the Wikipedia politicians dataset with the country population dataset, along with the predicted quality scores for each article. The columns in this file include:

    - country: The country associated with the politician's Wikipedia article.
    - region: The geographic region to which the country belongs.
    - population: The population of the corresponding country (in millions).
    - article_title: The title of the Wikipedia article.
    - revision_id: The revision ID of the article.
    - article_quality: The quality prediction of the article (e.g., FA, GA, B, C, Start, Stub).

2. `wp_countries-no_match.txt`
This text file contains a list of countries that were present in either the Wikipedia articles dataset or the population dataset, but not in both. Each unmatched country is output on a separate line.

3. `wp_errors.txt`
This file logs any articles for which the ORES API was unable to return a quality score. Each line contains information about the article's revision ID, name of the article, and error message.

4. `wp_article_per_capita.csv`
An intermediary file that calculates the number of Wikipedia articles per capita for each country with these columns:

    - country: The country.
    - number: The number of Wikipedia articles about politicians per person.

5. `wp_high_quality_article_per_capita.csv`
An intermediary file that calculates the number of high-quality articles per capita for each country. High-quality articles are considered as those with rating "FA" (Featured Article) or "GA" (Good Article). The columns of this file are:

    - country: The country.
    - number: The number of high-quality Wikipedia articles per person

**Considerations**
Wikipedia's folksonomic categorization system means there is little formal control over how pages are classified. As a result, some pages may not accurately reflect individual politicians or may include pages irrelevant to the analysis.

The ORES model used for predicting article quality is a machine learning tool and not always accurate.

The population and region data is from a different source compared to the politician data, so there are some unmatching countries.

**Analysis Output**    
The analysis produces tables to summarize and show statistics of coverage and quality of articles about politicians across nations and geographic regions. These tables are imbedded in the notebook.

1. **Top 10 Countries by Coverage**: A table listing the 10 countries with the highest number of articles per capita.
2. **Bottom 10 Countries by Coverage**: A table listing the 10 countries with the lowest number of articles per capita.
3. **Top 10 Countries by High-Quality Articles**: A table listing the 10 countries with the highest number of high-quality articles per capita.
4. **Bottom 10 Countries by High-Quality Articles**: A table listing the 10 countries with the lowest number of high-quality articles per capita.
5. **Geographic Regions by Total Coverage**: A ranked table by total articles per capita by region.
6. **Geographic Regions by High-Quality Coverage**: A ranked table by high-quality articles per capita by region.

## Steps
Steps to Run the Code in `wp_page_score_analysis.ipynb` 
   
This notebook is used for all the steps in the project, from making API requests to producing analysis output.
Locate the cell that defines configurations. Update the constants as needed for your data acquisition, such as the date range and any other relevant parameters.
Select "Run All".
The notebook will query the data for the specified articles, generate the datasets, and store the output files as described in the [Output Data Files](#output-data-files) section.

## Research Implications
From my findings, I was surprised to find that countries with large populations, such as China and India, have notably low coverage on English Wikipedia. This might to stem from China’s reliance on its own news platforms, which provide information that is more relevant and reliable for its citizens, suggesting a gap between global and local narratives. 

From my analysis, regions in Europe, America, and Oceania demonstrates higher coverage and quality in Wikipedia articles. This is expected, given that we are primarily examining an English-language platform. Interestingly, smaller countries with strong international ties, like Luxembourg, show high articles per capita and quality coverage, revealing a bias towards global visibility rather than population size. This reinforces that English Wikipedia favors English-speaking countries, indicating that it may not accurately represent global media creation and digital infrastructure. I believe researchers should consider supplementing their datasets with sources in other languages or from different platforms that might better capture the nuances of each country’s media landscape.

