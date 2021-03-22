# Movie Industry analysis for Microsoft

By: [Tamjid Ahsan](linkedin.com/in/tamjidahsan)
___
<img src="./assets/image_1.jpg"
     alt="Logo!"
     style="float: center; margin-center: 2px;">




# Overview

A handful of companies have defined the Hollywood film industry, dominating the US and world markets. They have weathered a world war, and a Great Depression and few moderate ones, innovated wide screen and color technologies, made peace with television, learned to exploit home video and online streaming, and are more powerful than ever before.

Most big corporations are already in this business or exploring feasibility of entry. Most of the major corporations operating only in this industry are thriving. 

# Business Problem

Microsoft sees all the big companies creating original video content and they want to get in on the fun. They have decided to create a new movie studio, but they don’t know anything about creating movies.

I am going to try to figure out what types of films are currently performing better at the box office. I shall recommend some actionable insights based on findings of this analysis, which the head of Microsoft's new movie studio can use to help decide what type of films to create.


<img src="./assets/image_0.png"
     alt="Logo!"
     style="float: center; margin-center: 10px;">

Areas of focus:

    * movie genres.
    * probability of success based on seasonality of releases.
    * profitability of movie franchise/film series.


# The Data

* [IMDb](https://www.imdb.com/) or <i>Internet Movie Database</i> was Originally a fan-operated website, now owned and operated by IMDb.com, Inc., a subsidiary of Amazon. This is one of the most reliable sourec for any information related movies in general. It is one of the most comprehensive dataset.
* [Box Office Mojo](https://www.boxofficemojo.com/) is also a part of IMDb.com, Inc., providing indepth financial informations among other metrics.
* [TMDb](https://www.themoviedb.org/) is a reliable source for movie related information. This is a popular user editable database for movies and TV shows.

Those three were used for sourcing data for the project as those are highly reliable sources without going for any paid service for information.
            

Data is collected from [IMDB website](https://datasets.imdbws.com) from downloadables, and scraping using [selenium](https://www.selenium.dev/) .
Additional data collected from TMDb using [API](https://www.themoviedb.org/documentation/api).
Then all of them are merged to create <b>'main_df'</b>, upon which this following analysis is performed.

## From IMDb

### Dataset from website

File containing detailed movie info inside [title.basics.tsv.gz](https://datasets.imdbws.com/title.basics.tsv.gz) was downloaded from `https://datasets.imdbws.com/title.basics.tsv.gz`

### Scraping using selenium

selenium is used to scrape data from [Box Office Mojo]('https://www.boxofficemojo.com/year/world/'). Years from 2014 to 2021 is scraped. Fetched information about world collection, international_collection, domestic_collection, and imdb_code.

Note: ***repo does not include temp files***

## From TMDb API

Information on same range of years was collected from TBDb using API.

# Preparing datasets

## IMDb
All data was merged to create the cleaned database.
### choosing features

*****Choosing to focus analysis on movies released between 2015 to 2020, where primary spoken language is English.*****

- In my opinion this is the most appropriate time frame to focus, as this gives enough data for analysis and at the same time does not include old info which will not be good representative of the current market situation. As customer/viewer taste and market trends shift over the time.

- Microsoft should focus only on releasing content in <b>English</b> for their kick-off. This gives them enough exposure and get noticed as a big player in the game, as they intend to be. Although they should focus on other territory to explore as there are ample opportunities left untapped. For example, in 2020 China surpassed North America in terms of industry value.\
As Microsoft has business across the globe, this should be relatively straight forward for them.

- I am also choosing not to focus on <b>ultra-low</b> budget movies for this analysis. Microsoft is one of the biggest corporations on earth. They have financial support to go for the big studios.
- I am also not including <b>'Documentary', 'Short', 'Adult', 'Reality-TV', 'Game-Show', 'Talk-Show', 'News', 'Film-Noir'</b> titles. Those are entirely different class of product to be compared with conventional movies.


# Exploratory data analysis

## EDA - top movie by return %
    
![png](./assets/output_161_0.png)
    


## EDA - top movie by gross profit



    
![png](./assets/output_163_0.png)
    


## EDA - profit by top 20 studio

>For competitor analysis and assessing market condition

![png](./assets/plt_go_1.png)



![png](./assets/plt_go_2.png)

Marvel Studios and Walt Disney has the best release count to world collection ratio. It took Universal Pictures way more budget to achieve the top spot.



![png](./assets/output_177_0.png)
    


***Note:*** One caveat of this graph is that because of the nature of the data, if a movie has multiple studios attached to it then all earnings of it is counted as the studios sole earnings. This is the reason why the mismatch of metrics. All things set aside, from this graph a visual understanding can be achieved about top studios without trying to make sense of the numbers. Turning off ylabels of first two plots can help on that regard. 

## EDA - Relation between subset of features

    Positive correlations:
              index                        feature_combo  correlation
    0     31  int_collection and world_collection     0.986302
    1     32  world_collection and dom_collection     0.955519
    2     41    int_collection and dom_collection     0.892850
    3     35      world_collection and vote_count     0.791444
    4     22            budget and int_collection     0.787109
    5     21          budget and world_collection     0.783042
    6     53        vote_count and dom_collection     0.773461
    7     44        int_collection and vote_count     0.763741
    8     23            budget and dom_collection     0.716023
    9     26                budget and vote_count     0.675298
    
     ----------------------------------------------------------------------
           Negative correlations:
              index                   feature_combo  correlation
    0      8        vote_count and startYear    -0.065041
    1      1    startYear and runtimeMinutes    -0.003422
    2      3  world_collection and startYear     0.024102
    3      4    int_collection and startYear     0.035525
    4      5    startYear and dom_collection     0.040447
    5      2            budget and startYear     0.053363
    6      7      vote_average and startYear     0.054454
    7     61     vote_average and popularity     0.156417
    8     15   runtimeMinutes and popularity     0.159567
    9     51   popularity and dom_collection     0.201020
    

### Findings and observation

From those table it can be observed that world collection, international collection and domestic collection is highly correlated. It is expected as world collection is a dependent variable of the other two. And the later two are highly correlated. This is also expected, as this is indicator of a profitable versus flop movie. Better performing movies has higher popularity as explained by world collection versus vote count, vice versa. High budget movies perform better overseas.

Overall budget is the key for indicating performance both in international and domestic performance and feedback from movie consumers. No other standout correlation was found. 

# Recommendations

## Which genre of movie to make, explained by top movie per genre by year

    
![png](./assets/output_196_0.png)
    


2015 was a good year for the industry. Animation has good performance but costly to make, hence lower percentage. Muscial had few good years then fell out of fashion. Action, Adventure, Family, Fantasy has been consistent performers. Horror and Mystery has high return percentage.

### Action suggestion

Any one or combination of Action, Adventure, Animation is recommended. Animation and Action has 35% chance for occurring as genre combo. There is no landslide winner here, although this graphs can be used to figure out which one to avoid, for example western and war. 

## Best time to release movie


- minor feature engineering

Release months are put in three bins based on market analysts opinion.The [dump months](https://en.wikipedia.org/wiki/Dump_months) are what the film community calls the two periods of the year when there are lowered commercial and critical expectations for most new releases from American filmmakers and distributors.

1. January - May: Dump month
3. June - July: Summer
3. August - October: Dump month
4. November - December: Holidays

    
![png](./assets/output_207_0.png)
    

    
2015's Summer was good in terms of percentage return but weirdly did not generate much cash. Releasing movie in the holidays season is the safest bet. But summer is having a consistent raise, except for 2020. 2020's summer was not normal by any means, thus this is expected. 





    
![png](./assets/output_209_0.png)
    


Movies released in holidays earn consistent returns but costs more. Summer is more dollar generating and volatile in a good way, on a uptrend.

    
![png](./assets/output_212_1.png)
    


Producing movies for summer release is more costly, but return is steeper. Number of movies beyond 500 million is more frequent as well as observation counts are higher for holidays release, and the line is flatter meaning less costly to produce. Holidays season is the better option.





    
![png](./assets/output_214_1.png)
    


Summer has the best earning potential. But line is steeper for holidays, confirming the point made on the previous graph.



    
![png](./assets/output_216_1.png)
    


Holidays movies are more popular and catch people on good mood maybe? Or content is less experimental. Reasoning can not be drawn from this figure but it can be said that holidays movies are more popular, which is good for entering the market with a more favorable impression on people.

### Action suggestion

My recommendation is to focus for release schedule in the holidays season. There is higher probability of financial and critical success for movies released in that time frame. It is relatively cheaper to make than the next best option; i.e., Summer.

## Franchise performance analysis leading to recommendation 


### Franchise info 

By franchise I mean serialization of movies either based on a related intellectual property or sharing same cinematic universe.


![png](./assets/df_graph_4.png)

    
Most franchise earn a lot on their investment. This is expected as there is a reason for film makers to visit same universe several times. More often than not it is because of their proven success record and popularity among movie consumers.





### Which genre to franchise
On an average films that are part of a franchaise earn 727.47% return.


![png](./assets/df_graph_3.png)
    
Observation: None of them fall into a single genre.


![png](./assets/plt_go_0.png)
Adventure, Action, Comedy market is saturated. Horror, Thriller, Mystery release count is lower with higher mean return percentage. This recommendation will alter if we look at collection instead of ROI% because those genre requires less budget, so the return percentage is generally higher. 

### non franchise info




    
![png](./assets/output_243_0.png)
    





    
![png](./assets/output_244_0.png)
    


Non franchised movies are experiencing a hard time in the box office. The general trend is downwards across the board except Crime and Drama and Mystery. Mystery, Sci-Fi and Horror did well in 2020. Those three genres have high correlation.


### Side by side 

    
![png](./assets/output_250_0.png)
    



    
![png](./assets/output_250_1.png)
    


Franchised movies are often more popular with greater success in international market.



    
![png](./assets/output_252_0.png)
    


Franchised movies require bigger budget but their return is also significantly higher.



    
![png](./assets/output_254_0.png)
    


This straightforward time series of box office gross profit of the two categories is the simplest but most layman friendly chart that demonstrate the stark difference between them. Franchised movies are consistently outperforming the other category.

### Action suggestion

All the analysis leads towards starting a movie franchise in a shared movie universe. This must be be priority when selecting genre, director and other crew and cast. There must be option for serialization in the future. And for this Horror, Thriller, Mystery and Adventure, Action, Comedy  genre should be prioritized. It very rare that a movie falls in only one genre this days.

# Conclusion

Lets summarize and reiterate:
***
1. My recommendation is to focus for release schedule in the ***holidays season***. There is higher probability of financial and critical success for movies released in that time frame. It is relatively cheaper to make than the next best option; i.e., Summer.

2. Any one or combination of ***Action***, ***Adventure***, ***Animation*** is recommended. Animation and Action has 35% chance for occurring as genre combo. There is no landslide winner here, although this graphs can be used to figure out which one to avoid, for example western and war. 

3. All the analysis leads towards starting a ***franchise*** in a shared movie universe. This must be be priority when selecting genre, director and other crew and cast. There must be option for serialization in the future. And for this ****Horror, Thriller, Mystery**** or ****Adventure, Action, Comedy**** genre combination should be prioritized. 
    
    It very rare that a movie falls in only one genre this days.

# Next Steps

Further analyses could yield additional insights to further improve considerations for creating a new movie:
***

- Performance of **other** language movies and markets.
- Focusing on **low budget movies versus high budget movies** performance and rational.
- Movies performance in **home and international market**. 
- Recommending **lead director**.
- Recommending **movie cast** classified on genre.
- Focus only on **2020** data and find pattern and trend.

# For More Information

See the full analysis in the [Jupyter Notebook](./student.ipynb) or review this [presentation](./presentation.pdf).

# Appendix

## Most produced genre combo


    Positive correlations:
              index            feature_combo  correlation
    0    359        Musical and Music     0.552813
    1     38  Adventure and Animation     0.353164
    2    316       Horror and Mystery     0.242051
    3      1     Adventure and Action     0.234557
    4     50    Biography and History     0.203732
    5    256      Thriller and Horror     0.199766
    6      7         Action and Crime     0.184287
    7    255     Thriller and Mystery     0.176246
    8     29     Adventure and Family     0.157636
    9    198     Animation and Family     0.140764
    
     ----------------------------------------------------------------------
           Negative correlations:
              index        feature_combo  correlation
    0     65     Comedy and Drama    -0.290930
    1    112  Comedy and Thriller    -0.248184
    2     78  Animation and Drama    -0.203516
    3     23  Adventure and Drama    -0.191267
    4     76     Horror and Drama    -0.184330
    5      3     Action and Drama    -0.155409
    6    116    Comedy and Horror    -0.150491
    7    115   Comedy and Mystery    -0.148315
    8      5    Comedy and Action    -0.134239
    9      8   Action and Romance    -0.124091
    

## Variability of profitability on different metrics

### budget vs profitability



    
![png](./assets/output_269_0.png)
    


### runtime on profitability





    
![png](./assets/output_271_0.png)
    


### user rating on profitability



    
![png](./assets/output_273_0.png)
    

