## Battle of Neighborhoods (Week 2)
### by Alberto Iriberri (Dec 2019)

# The project (Jupyter Notebook)
You can find the Jupyter Notebook that I used to ellaborate the data and reach the final conclussions here:

[Los Angeles New restaurant Project](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LosAngelesFoursquareAndGeo.ipynb)

and also you may find interesting the Notebook I programmed to specifically extract Los Angeles data from the Wikipedia:

[Los Angeles Wikipedia Extractor](https://github.com/pangodream/Coursera_Capstone/blob/master/Battle_of_Neighborhoods/Week_2/LANBExtractor.ipynb)

# Report
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





