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
   

   
   
5. 
   


# Fields of Data Files



# Known issues/special considerations

# Directory of the Repo


# Visualizations
