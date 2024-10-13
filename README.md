# data-512-homework_2
Data 512 HW2: Considering Bias in Data

## Goal
We aim to explore the concept of bias in data using Wikipedia articles on political figures from different countries

## License
Source Data: Wikimedia/Wikipedia \
[politicians_by_country_AUG.2024.csv](politicians_by_country_AUG.2024.csv)
[population_by_country_AUG.2024.csv](population_by_country_AUG.2024.csv)

[Creative Commons Attribution-ShareAlike 4.0 International License ("CC BY-SA 4.0")](https://creativecommons.org/licenses/by-sa/4.0/deed.en), and
[GNU Free Documentation License ("GFDL")](https://www.gnu.org/copyleft/fdl.html) (unversioned, with no invariant sections, front-cover texts, or back-cover texts).

 According to the ToU, all content contributed to or derived from Wikimedia Projects, including usage data like pageviews, is shared freely under a Creative Commons Attribution-ShareAlike license (CC BY-SA). This means my datasets, which includes publicly available pageview data, must also be freely accessible and properly attributed, ensuring that any reuse or modification of the dataset remains open and shared under the same or compatible terms.

## Pageviews API Documentation
[Documentation](https://doc.wikimedia.org/generated-data-platform/aqs/analytics-api/reference/page-views.html)

## Intermediate File
1. [lists.json](lists.json): records `Article Title`, `Article Revision ID`, and `Article Score` to avoid re-running the Wikimedia API

## Output Files
1. [wp_countries-no_match.txt](wp_countries-no_match.txt): countries with no match in either politician and population csv files.
2. [wp_politicians_by_country.csv](wp_politicians_by_country.csv): merged politician articles with population data in the following format
```
| country | region | population | article_title | revision_id | article_quality |
```

## Embedded Result Tables
1. **Top 10 countries by coverage**: The 10 countries with the highest total articles per capita (in descending order)
2. **Bottom 10 countries by coverage**: The 10 countries with the lowest total articles per capita (in ascending order)
3. **Top 10 countries by high quality**: The 10 countries with the highest high quality articles per capita (in descending order)
4. **Bottom 10 countries by high quality**: The 10 countries with the lowest high quality articles per capita (in ascending order)
5. **Geographic regions by total coverage**: A rank ordered list of geographic regions (in descending order) by total articles per capita
6. **Geographic regions by high quality coverage**: Rank ordered list of geographic regions (in descending order) by high quality articles per capita


## Data Issues
- Some countries in the [politicians_by_country_AUG.2024.csv](politicians_by_country_AUG.2024.csv) are called/labeled differently than in the [population_by_country_AUG.2024.csv](population_by_country_AUG.2024.csv). For example, in the politician table, South Korean politicians are labeled to be in 'Korea, South' or 'Korean', whereas in the population table, South Korea is labeled as 'Korea (South)'. This difference caused the mismatch when merging on the two dataframes on country.

## Research Implications
1. What you have learned, what you have found, what (if anything) surprised you about your findings, and/or what theories you have about what nay biases might exist \
Based on the two dataset provided, the wikimedia API, and the ORES scores through LiftWing ML Service API, we gained further understanding on the quantity and quality of politicians wikipedia articles across different countries. In the result section, we are primarily interested in the total articles per capita (a ratio representing the number of articles per person) and high quality articles per capita (a ratio representing the number of high quality articles per person) on a country-by-country and regional basis. Interestingly, in the top 10 countries by coverage analysis, Monaco and Tuvalu are ranked as the top two since the population size in the [population_by_country_AUG.2024.csv](population_by_country_AUG.2024.csv) is 0, yielding an 'inf' coverage. Additionally, if we ignored the two countries, all the other 10 countries have relatively low raw article counts (max is 44 articles for Bhutan politicians) but since the population of each respective country is so small, the article coverage is high. Similar trends are observed in the ratio of high quality articles per person tables. 
Moreover, it is clear that there are more articles for European politicians than other regions. There also seem to not have any North American politicians in the dataset, so there might be a regional bias there. Lastly, high quality articles are in English, which might introduce a linguistic bias, as countries where English is not the primary language could have fewer high-quality articles due to limited contributions from native speakers or challenges in accessing reliable, localized sources for verification. This could disproportionately impact the representation and quality of political figures from non-English-speaking regions.

## Q&A
1. What biases did you expect to find in the data (before you started working with it), and why? \
Before looking at the datasets, I expected to see a lot of articles on European, American, or more controversial politicians. Since Wikipedia tends to cater more to English speakers, I figured politicians who are more well-known or interesting to an English-speaking audience would have more articles. This might mean other regions or less globally known politicians could be underrepresented.

2. What (potential) sources of bias did you discover in the course of your data processing and analysis? \
In the course of data processing and analysis, several potential sources of bias were discovered. First, the dataset doesn't include all politicians that have ever existed, and notably, there were no North American politicians, which introduces a regional bias by excluding an entire geographic area. This absence could skew any conclusions about global political coverage on Wikipedia. 
Additionally, discrepancies in how countries are named between the politician dataset and the population table introduced matching issues. For instance, South Korean politicians were labeled as "Korean" and "Korea, South" in the politician dataset, while the population table labeled the country as "Korea (South)". This inconsistency made it difficult to accurately match politicians to their respective population data, potentially leading to errors in coverage analysis by country.
These issues suggest that the data may not be entirely representative, and the way regions and countries are labeled can introduce bias in the analysis, especially when merging datasets.

3. What might your results suggest about (English) Wikipedia as a data source? \
In exploring the quality of Wikipedia politician articles, we found that only 303 out of 7155 articles are considered as "high quality" (GA and/or FA), which is about 4.23%. This suggests that the majority of English Wikipedia articles may not be as reliable or well-sourced, which could make Wikipedia a less dependable data source for certain kinds of research. However, since these articles are ranked based on their quality, focusing on GA/FA articles can still provide reliable and trustworthy information.
