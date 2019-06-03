# Project 4: A Data Analysis of the Camp Fire

### Anne Kerr, Michel Elias, Hugo Delgado, Stephen Godfrey, DSI-CC7-San Francisco

### Problem Statement

Use data to quantify the Camp Fire to prototype models that could be employed during a wildfire response.



### Executive Summary

The Camp Fire was perhaps the most destructive recorded wildfire in California's history and was one of the world's most destructive natural disasters in 2018.  All totaled, it burned over 153,000 acres and destroyed over 13,500 structures [Camp Fire](https://en.wikipedia.org/wiki/Camp_Fire_(2018)) and [Cal Fire Incident](http://cdfdata.fire.ca.gov/incidents/incidents_details_newsreleases?incident_id=2277).  The fire began on November 8, 2018 and was not 100% contained until November 25, 2018.  During that time, the event was a social media and news topic of substantial interest, and it was widely covered on both media platforms.

<img src="./images/CampFireMapNov20Tweets.png" alt="Process" width="600"/>

In this project, we collect data from several sources to quantitatively analyze and model the fire.  Specifically, we use methods of fundamental Exploratory Data Analysis (EDA) and machine learning modeling to prototype techniques that could be built into a fire monitoring tool and serve as an additional source of event information for use in responding to similar disasters.

Our approach was to collect data from a wide range of sources, to clean and store that data such that they could be used for analysis and then to feed them into models to measure their usefulness in explaining the size of the fire.  Within our EDA work, we track metrics and map information showing the incident's progression over its life.  

Our approach to modeling is to use three techniques of Natural Language Processing (NLP) to group tweet and news stories into related categories based on their contents.  We then combine these data elements with progression metrics (structures destroyed, fatalities, etc) to create a modeling dataset.  This dataset was then examined using a range of regression models to measure its effectiveness in explaining the size of the fire. 



### Conclusions and Recommendations

While this analysis was limited and exclusive to a single event, the Camp Fire, and the dataset was constructed after its conclusion, we find some useful results.  These resulting observations are helpful in prototyping and in setting a direction for further analysis, but the dataset needs to be expanded to include additional fire events and to incorporate information as it would actually be available during incidents before they can be considered conclusive.

Key findings include

* Combining progression metrics such as fatalities and the number of affected structures with news and tweet data seem to provide better models for the size of the fire than simply using progression metrics alone suggesting that there is value in systematically monitoring such sources during the course of an event,

* Categorizing tweet and news data into relatively small groupings (in this case 10) appears to be a useful way to employ such information when using them to explain fire progression,

* Incorporating the location of tweets into monitoring tools present challenges since many tweets do not contain geographical coordinates and many of the profile locations were far from the fire,   

* Choosing NLP models depends on the type of text with Latent Dirichlet Allocation (LDA) and Singular Value Decomposition (SVD) with K-Means Clustering performing best for tweets and news stories respectively, 

* Selecting regression models relies on several considerations with Random Forest Regressors in which models were allowed to split data using a combination of factors performing the best in this analysis.

We believe that this approach would benefit from further analysis including

* Building and testing similar datasets for other fires ideally in geographically diverse locations,

* Gathering data such that the time intervals (in this case 12 hours) could be divided into more granular windows allowing for the modeling of fast-moving events,

* Obtaining data seen by emergency response teams as the disaster unfolds to further delineate the type and availability of information during the course of such events, 

* Employing a wider range of models such as Bayesian Inference approaches to establish prior and posterior distributions of some of the key parameters.



### Data

#### Data sources:

* Cal Fire's [incident reports](http://cdfdata.fire.ca.gov/incidents/incidents_details_newsreleases?incident_id=2277) were used to gather fire-progression metrics.

* Twitter's [Premium Search API](https://developer.twitter.com/en/docs/tweets/search/api-reference/premium-search) was used to pull tweet data related to the Camp Fire.

* The [News API](https://newsapi.org/) was used to pull news stories covering the Camp Fire.

* Geospatial Multi-Agency Coordination [GeoMac](https://www.geomac.gov/) [services](https://rmgsc.cr.usgs.gov/outgoing/GeoMAC/2018_fire_data/California/Camp/) were used to construct perimeter maps.

* National Interagency Fire Center ([NIFC](https://nifc.maps.arcgis.com)) mapping [tools](https://nifc.maps.arcgis.com/apps/webappviewer/index.html?id=41fe4499192a4e008a1d0c69a96d6284) and Cal Fire mapping [tools](https://calfire-forestry.maps.arcgis.com/apps/webappviewer/index.html?id=5306cc8cf38c4252830a38d467d33728&extent=-13547810.5486%2C4824920.1673%2C-13518764.4778%2C4841526.1117%2C102100) were used to construct fire perimeter data.

* Federal Emergency Management Agency ([FEMA](https://www.fema.gov/)) data and [press releases](https://www.fema.gov/news-release/2019/01/11/4407/nearly-350-million-federal-grants-and-loans-wildfire-survivors) and U.S. Federal Government Spending and Grants [data](https://www.usaspending.gov/#/) were used to estimate total Federal-level costs.
 


#### Modeling data dictionary:

|Column           |Description         |
|-----------------|--------------------|
|date (index)| date and time of incident report|
|unified_command_agencies|response agencies|
|incident_location|description of incident location|
|size_acre| size of the fire (acres)|
|containment| containment percentage|
|expected_full_containment| expected date for full containment|
|civilian_fatalities| count of civilian fatalities|
|firefighter_injuries| count of firefighter injuries|
|structures_threatened| count of threatened structures|
|single_residences_destroyed| count of destroyed single residences|
|single_residences_damaged| count of damaged single residences|
|multiple_residences_destroyed| count of destroyed multiple residences|
|commercial_destroyed| count of destroyed commercial properties|
|commercial_damaged| count of damaged commercial properties|
|other_minor_structure_damaged| count of damaged other properties|
|situation_summary| text summary of the current situation|
|evacuations_orders| text summary of evacuation orders|
|evacuation_warning| text summary of evacuation warning|
|forest_closures| text summary of forest closures|
|evacuation_centers| names and addresses of  evacuation centers|
|road_closures| text description of road closures|
|engines| count of engines|
|water_tenders| count of water tenders|
|helicopters| count of helicopters|
|hand_crews| count of hand crews|
|dozers| count of dozers|
|total_personnel| count of total personnel|
|air_tankers| text description of air tankers|
|cooperating_agencies| names of cooperating agencies|
|lda_t_*| Tweet group counts using the LDA approach [* 0:9]|
|svdc_t_*| Tweet group counts using the SVDC approach [* 0:9]|
|d2vc_t_*| Tweet group counts using the d2vc approach [* 0:9]|
|lda_n_*| News group counts using the LDA approach [* 0:9]|
|svdc_n_*| News group counts using the SVDC approach [* 0:9]|
|d2vc_n_*| News group counts using the d2vc approach [* 0:9]|

