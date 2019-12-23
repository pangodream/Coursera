## Battle of Neighborhoods (Week 2)
### by Alberto Iriberri (Dec 2019)

# The project (Jupyter Notebook)
You can find the Jupyter Notebook that I used to ellaborate the data and reach the final conclusions here:

[Los Angeles New restaurant Project](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LosAngelesFoursquareAndGeo.ipynb)

and also you may find interesting the Notebook I programmed to specifically extract Los Angeles data from the Wikipedia:

[Los Angeles Wikipedia Extractor](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LANBExtractor.ipynb)

# The presentation
[Regression to Pasta PDF](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/Regression%20to%20Pasta.pdf)

[Regression to Pasta Powerpoint](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/Regression%20to%20Pasta.pptx?raw=true)

# The Report
## 1.- Introduction (Business requirements)
As we discussed in the orevious week project, the main goal of this project is to find a good opportunity in Los Angeles, CA for opening a new restaurant.

We need to take into account that Los Angeles is multi-cultural city (probably one of the most diverse in the world) and opening a new restaurant may be a financial risk if you don't measure all the different variables.

Our financial partners don't need to start a restaurant for an specific food type. They have the money to start a new business and they think a restaurant in LA, where they have their headquarters, could be a good choice.

Based on that, we need to accomplish two requirements and use available free internet data:
1. Select the **food type** for our restaurant
2. Choose the **neighborhood** where we wil place our restaurant

## 2.- Data Requirements
We will retrieve our data from two different sources:
* **Wikipedia**: list of Los Angeles neighborhoods & districts
* **Foursquare**: list of restaurants for each of the neighborhoods

_We will also use Nominatim API to get geographic coordinates for each place_

## 3.- Data understanding
* List of neighborhoods:

We need to clean or remove those districts that seem to have incorrect information in Wikipedia. After analyzing each of them, it is not relevant to remove part of them as they are only small zones. Note that even we remove a small district, their restaurants will be in the venues list because they are enough close to another main district or neighborhood.

* List of venues (restaurants):

Though we specified **Restaurant** as the query for Foursquare API it returns some venues that are not really restaurants. We have to detect these cases and axclude them from the final list.

* Coordinates (GEO):

Some of the places are not geolocated. As we did with incorrect neighborhoods, we remove these places.

## 4.- Data preparation
**Nominatin API problems**

As we mentioned above, we are using Nominating to get the GEO coords for all the places we will analyze. When we iterate the list of places and invoke Nominnating API, we get a **Service unavailable** error.

We dealt with this problem in the next way:
* Set a delay of 1 second between each invocation
* Save the results we get (for every coordinates we get) so that we don't need to repeat the process for the same items

Data filtering and transformation will be done always on the origina data, and not on data previosly transformed or manipulated. This will allow us to perform as many tests as we need without the need of retrieving the original data again.

The original data is contained in two different csv files:

* [Neighborhoods .csv file](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LosAngeles.csv)
* [Venues .csv file](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LosAngelesVenues.csv)

## 5.- Methodology
To better understand the field and the problem we have to solve, we need to use visual tools that help us to make decissions.

First we will classify the data we have to understand which are the LA people preferences. For instance, probably we will not find any Scotish restaurant (or very few) but a bunch of Mexican or Latin restaurants.

Once we know the preferences we will choose a restaurant of this type based on these:

**If we choose a type of food that LA people doesn't like now, we will have no competitors, but also we will have no customers**

**If we choose a type of food that LA people like now but we place it where there are a lot of competitors with the same food type, we will not have a lot of customers**

**We need to place a restaurant specialized in a food type that LA people likes in a neighborhood with few competitors. Does this exist?**

We need two tools for our purpose:
* **Ranking tools**: Python Pandas and Numpy will be enough
* **Clustering tools**: As we are clustering based on geographic coordinates it is recommendable to use DBSCAN algorithm

So, the steps to reach our conclusions will be:
1. Rank all the food types in LA to know what customers like
2. Select our top n food types to make the clustering analysis with
3. Select all the existing restaurant for the selected categories and place it in the map
4. Use clustering tools to divide the map into different numbered clusters
5. Classify food types / clusters using a weighted matrix
6. Analyze with maps and the matrix which are our options
7. Make a decission/recommendation

## 6.- Modeling
**Important:** Take into account that the details of the data modeling/analysis are contained in the Notebook. Here I will only place the images to easily explain the process**

### 6.1 The restaurants dataframe
![Restaurants dataframe](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LA_RestaurantsDataframe.png?raw=true)

### 6.2 Choosing the top n food types
![Food types histogram](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LA_top_7.png?raw=true)
![Top 7 Food types](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LA_Top_7_list.png?raw=true)

### 6.3 Map distribution of top 7 food types restaurants
![Map distribution of top 7](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LA_Rest_types.png?raw=true)

### 6.4 Clustering places with DBSCAN
![Map distribution of top 7](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LA_Clusters.png?raw=true)

### 6.4.1 Cluster 0
![Cluster 0](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LA_Cluster_00.png?raw=true)

### 6.4.1 Cluster 1
![Cluster 1](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LA_Cluster_01.png?raw=true)

### 6.4.1 Cluster 2
![Cluster 2](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LA_Cluster_02.png?raw=true)

### 6.4.1 Cluster 3
![Cluster 3](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LA_Cluster_03.png?raw=true)

### 6.4.1 Cluster 4
![Cluster 4](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LA_Cluster_04.png?raw=true)

### 6.4.1 Cluster 5
![Cluster 5](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LA_Cluster_05.png?raw=true)

### 6.4.1 Cluster 6
![Cluster 6](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LA_Cluster_06.png?raw=true)

### 7 Type of Food x Cluster Matrix
![7 Type of Food x Cluster Matrix](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/Cross_Type_Cluster.png?raw=true)

### 8 Final Analysis
![8 Final Analysis 1](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LA_Clusters_1_2_3_6.png?raw=true)
![8 Final Analysis 2](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/WeightedResults.png?raw=true)

## The weighted matrix shows that Cluster 1 and Cluster 2 are very good places to set an Italian Restaurant
They are residential zones, and in the middle of both there is a hospital, what can bring us a lot of potential customers.
![The place](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/Environment.png?raw=true)
![The place map](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/PlaceMap.png?raw=true)

## Our final recommendation
Buying a residential house in the specified place and set an Italian restaurant.
The name of the restaurant could be **Regression to pasta**



