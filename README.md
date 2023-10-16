# data-512-homework_2

# Goal of the Project

The goal of this project is to explore the concept of bias in data using articles about cities in different U.S. states, which we could obtain from Wikipedia. In order to investigate further, we combineed the dataset of Wikipedia articles with a dataset of state populations and the regions to which each state belongs to, and use ORES (a machine learning service) to estimate the quality of the articles about the cities.

The analysis will consists of three parts:

**The states with the greatest and least coverage of cities on Wikipedia compared to their population.**

**The states with the highest and lowest proportion of high quality articles about cities.**

**A ranking of US geographic regions by articles-per-person and proportion of high quality articles.**

# License Used

## Tools/API used

**Wikimedia**:  to extract the page information of articles. [Sample code used in this project comes from here](https://drive.google.com/file/d/15UoE16s-IccCTOXREjU3xDIz07tlpyrl/view?usp=sharing)

**ORES model**: provides the peer reviewed score of each article based on the quality. [Sample code used in this project comes from here](https://drive.google.com/file/d/17C9xsmR9U3lJeD52UTbAedlHDetwYsxs/view?usp=sharing)

## Data files to start with

**us_cities_by_state_SEPT.2023.csv**: the names/urls of the articles we would be working with. This data is scraped from [this WikiPedia page](https://en.wikipedia.org/wiki/Category:Lists_of_cities_in_the_United_States_by_state) and the scraped result could be found [here](https://drive.google.com/file/d/1khouDmMaZyKo0y5WkFj4lu7g8o35x_98/view?usp=sharing)

**NST-EST2022-ALLDATA.csv**: this data is obtained from [here](https://www.census.gov/data/tables/time-series/demo/popest/2020s-state-total.html). I chose the full dataset instead of the excel file because the excel file is not in a table. I took out only the names of states and the estimated population of the states for the analysis

**US States by Region in Table - US Census Bureau.csv**: the original dataset *US States by Region - US Census Bureau.csv* comes from [this file](https://docs.google.com/spreadsheets/d/14Sjfd_u_7N9SSyQ7bmxfebF_2XpR8QamvmNntKDIQB0/edit?usp=sharing)

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

   *Last but not least, while taking out the duplicated rows should have been done in the first step, it is instead done here.*
   
5. The final dataset *wp_scored_city_articles_by_state.csv* is produced in the *data analysis.ipynb* since an extra field was required to testify the differences between populations from own calculation and the US Census Bureau



# Fields of Data Files

The final dataset contains of fields of

**state** - the name of the sata

**regional_division** - the region to which the state belongs

**population** - the estimated population of the state in 2022

**article_title** - title of the article that's related to the state

**revision_id** - revision id of the article, which allowed us to obtained reviewed scores from ORES 

**article_quality** - the predicted reviewed scores from ORES


# Known issues/special considerations

There exist some states missing from [the scraped dataset](https://drive.google.com/file/d/1khouDmMaZyKo0y5WkFj4lu7g8o35x_98/view?usp=sharing) and thus some states are being missed out in this analysis. Further, the data of regional population from [the Census Bureau](https://docs.google.com/spreadsheets/d/14Sjfd_u_7N9SSyQ7bmxfebF_2XpR8QamvmNntKDIQB0/edit?usp=sharing) might not fully align with the calculated results from the final dataset obtained using code files here. While it is assumed that we should keep on using the final dataset obtained from the code files, three regions out of four have different total populations than the ones from the Census Bureau. The differences were located however, while two regions have different populations due to the missing of two states from [the scraped dataset](https://drive.google.com/file/d/1khouDmMaZyKo0y5WkFj4lu7g8o35x_98/view?usp=sharing), the other's difference comes from that Census Bureau took District of Columbia into account when measuring regional population. Again, in order to stick to the dataset obtained from the code files, here we used the calculated regional population from the final dataset.

# Research Implications

From this project, I was surprised to find that West Region came to the last when looking at the total coverage per capita considering the great population on the West Coast and the burgeoning of cutting-edge technologies. However, it might at the same time be highly reasonable since West Coast in general has a shorter history comparing to other regions especially Northeast Region and thus might not have so many pages to cover the historical events. Meanwhile, since we are only looking at the information at the level of per capita, the greater population might have the opposite effects on the per capita. 


What (potential) sources of bias did you discover in the course of your data processing and analysis?

In the course of my data processing and analysis, I found that two states, i.e. Connecticut and Nebraska, were missing from the dataset even though they are listed in the [Wikipedia page](https://en.wikipedia.org/wiki/Category:Lists_of_cities_in_the_United_States_by_state) at the top.


What might your results suggest about (English) Wikipedia as a data source?

California has a concentration of Hispanic population, which indicates that it is possible for the residents to use languages other than English, such as Spanish, to edit Wikipedia articles about the cities or even create and edit articles on websites that are more open to other languages. Therefore, using (English) Wikipedia as a data source, or using only (English) Wikipedia as the data source, would possibly cause the ignoring of the potential contribution of the residents and further the bias in our analysis.


Can you think of a realistic data science research situation where using these data (to train a model, perform a hypothesis-driven research, or make business decisions) might create biased or misleading results, due to the inherent gaps and limitations of the data?

Consider a company that is thinking of putting its advertisement on Wikipedia. To begin with, they might miss out the two states that are missing from the scraped data and missing a large population as its audience. Further, by looking at the per capita for the article coverage, the company might intuitively consider the states/regions with higher number in per capita will naturally have more people going onto the webpage to edit and to contribute, and thus there ill be higher chance for more people to see the advertisement, and so decide to put more efforts/money to the advertisement posted there. However, the higher figure in per capita might only reflect the fact that there could be a longer history in the area thus there is a higher number in the total articles leading to the higher per capita. Thus the business decision driven by the data in this case might be misled.


# Directory of the Repo
```bash
.
├── LICENSE
├── README.md
├── data analysis.ipynb
├── data preparation cleaned.ipynb
├── data preparation.ipynb
├── raw data
│   ├── cities_by_state.json
│   ├── score_first_attemp.csv
│   ├── updated_score.csv
│   └── wp_scored_city_articles_by_state_pre.csv
├── results (table)
│   ├── bottom10.png
│   ├── bottom10_high.png
│   ├── coverage_region.png
│   ├── coverage_region_bureau.png
│   ├── high_region.png
│   ├── high_region_bureau.png
│   ├── top10.png
│   └── top10_high.png
└── wp_scored_city_articles_by_state.csv
```

# Tables

**The Top 10 Coverage by States**

<img width="386" alt="top10" src="https://github.com/hww1999/data-512-homework_2/assets/50925030/2f6ca292-dadd-4d2c-9cdb-f99d89fd241a">

**The Bottom 10 Coverage by States**

<img width="371" alt="bottom10" src="https://github.com/hww1999/data-512-homework_2/assets/50925030/d3ecffbc-ee45-4e3e-97a8-f5d6e32e8e20">

**The Top 10 High Quality Coverage by States**

<img width="371" alt="top10_high" src="https://github.com/hww1999/data-512-homework_2/assets/50925030/66e6c401-20c7-46ff-9bfd-b7605734d975">

**The Bottom 10 High Quality Coverage by States**

<img width="376" alt="bottom10_high" src="https://github.com/hww1999/data-512-homework_2/assets/50925030/a261b546-f569-46a0-ad25-59c33fabb9f9">

**The Coverage by Regions (in descending order)**

**Using the population data from the US Census Bureau**

<img width="519" alt="fa84ac3a00a8269032a501434cb0ea7" src="https://github.com/hww1999/data-512-homework_2/assets/50925030/01a2572d-bd71-4703-a3c2-d8a17ce7aa32">

**Using the population data from the final dataset with further calculation**

<img width="348" alt="157e30db29d73f3ea67df5726e1590d" src="https://github.com/hww1999/data-512-homework_2/assets/50925030/cca9befe-d655-46fc-95fe-cdffb5914b96">


**The High Quality Coverage by Regions  (in descending order)**

**Using the population data from the US Census Bureau**

<img width="524" alt="b67ca27eaa1e40598f9fb89ca9b4384" src="https://github.com/hww1999/data-512-homework_2/assets/50925030/0a97dc44-7661-4633-b9a7-2a580f6e9173">

**Using the population data from the final dataset with further calculation**

<img width="345" alt="3208bb1cf6f95adc98ab9fc8d205b7e" src="https://github.com/hww1999/data-512-homework_2/assets/50925030/b8000874-2bb4-4387-adfd-df439fb59dd7">

