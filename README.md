# data-512-homework_2

# Goal of the Project

The goal of this project is to explore the concept of bias in data using articles about cities in different U.S. states, which we could obtain from Wikipedia. In order to investigate further, we would combine the dataset of Wikipedia articles with a dataset of state populations, and use ORES (a machine learning service) to estimate the quality of the articles about the cities.

The analysis will consists of three parts:

**The states with the greatest and least coverage of cities on Wikipedia compared to their population.**

**The states with the highest and lowest proportion of high quality articles about cities.**

**A ranking of US geographic regions by articles-per-person and proportion of high quality articles.**

# License Used

ORES

MediaWiki REST API

The US Census Bureau

# Data Preprocessing Steps

1. obtained page information using WikiMedia - resulted in cities_by_state.json with 22157 rows of data and fields of (bolded fields are retained):
   
   **pageid**, 
   ns, 
   **title**, 
   contentmodel, 
   pagelanguage, 
   pagelanguagehtmlcode, 
   pagelanguagedir, 
   touched, 
   **'lastrevid'**, 
   length, 
   **talkid**, 
   fullurl, 
   editurl, 
   canonicalurl, 
   watchers, 
   redirect, 
   new
3. Using personal access token and **lastrevid** from cities_by_state.json to obtain ORES score of articles

   *During the first attempt to get the scores, 107 articles failed to get the scores, which are mainly regions in Stata Michigan and the score value are put in **REQUEST FAIL** to distinguish from articles that succeeded in the first attempt*
   
   *In the second attempt, 106 out of the 107 succeeded in retrieving the scores, and the only one left has duplicated **pageid** and **title** in the dataframe but with a different **lastrevid** and obtained score*
   
![failAttempt](https://github.com/hww1999/data-512-homework_2/assets/50925030/aef07b9e-42f2-4bc5-8baa-2143685f9efc)

   
   
5. 
   


# Fields of Data Files



# Known issues/special considerations

# Research Implications

From this project, I was surprised to find that West Region came to the last when looking at the total coverage per capita considering the great population on the West Coast and the burgeoning of cutting-edge technologies. However, it might at the same time be highly reasonable since West Coast in general has a shorter history comparing to other regions especially Northeast Region and thus might not have so many pages to cover the historical events. Meanwhile, since we are only looking at the information at the level of per capita, the greater population might have the opposite effects on the per capita. 


What (potential) sources of bias did you discover in the course of your data processing and analysis?

In the course of my data processing and analysis, I found that two states, i.e. Connecticut and Nebraska, were missing from the dataset even though they are listed in the [Wikipedia page](https://en.wikipedia.org/wiki/Category:Lists_of_cities_in_the_United_States_by_state) at the top.


What might your results suggest about (English) Wikipedia as a data source?

California has a concentration of Hispanic population, which indicates that it is possible for the residents to use languages other than English, such as Spanish, to edit Wikipedia articles about the cities or even create and edit articles on websites that are more open to other languages. Therefore, using (English) Wikipedia as a data source, or using only (English) Wikipedia as the data source, would possibly cause the ignoring of the potential contribution of the residents and further the bias in our analysis.


Can you think of a realistic data science research situation where using these data (to train a model, perform a hypothesis-driven research, or make business decisions) might create biased or misleading results, due to the inherent gaps and limitations of the data?

Consider a company that is thinking of putting its advertisement on Wikipedia. To begin with, they might miss out the two states that are missing from the scraped data and missing a large population as its audience. Further, by looking at the per capita for the article coverage, the company might intuitively consider the states/regions with higher number in per capita will naturally have more people going onto the webpage to edit and to contribute, and thus there ill be higher chance for more people to see the advertisement, and so decide to put more efforts/money to the advertisement posted there. However, the higher figure in per capita might only reflect the fact that there could be a longer history in the area thus there is a higher number in the total articles leading to the higher per capita. Thus the business decision driven by the data in this case might be misled.


# Directory of the Repo


# Visualizations
