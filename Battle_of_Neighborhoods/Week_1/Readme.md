## Battle of Neighborhoods (Week 1)
### by Alberto Iriberri (Dec 2019)

## 1.- Introduction / Business problem
The main goal of this project is to find a good opportunity in Los Angeles, CA for opening a new restaurant.

We need to take into account that Los Angeles is multi-cultural city (probably one of the most diverse in the world) and opening a new restaurant may be a financial risk if you don't measure all the different variables.

Our financial partners don't need to start a restaurant for an specific food type. They have the money to start a new business and they think a restaurant in LA, where they have their headquarters, could be a good choice.

Based on that, we need to accomplish two requirements and use available free internet data:
1. Select the **food type** for our restaurant
2. Choose the **neighborhood** where we wil place our restaurant

## 2.- Data 
We will retrieve our data from two different sources:
* **Wikipedia**: list of Los Angeles neighborhoods & districts
* **Foursquare**: list of restaurants for each of the neighborhoods

_We will also use Nominatim API to get geographic coordinates for each place_

* List of neighborhoods:

We need to clean or remove those districts that seem to have incorrect information in Wikipedia. After analyzing each of them, it is not relevant to remove part of them as they are only small zones. Note that even we remove a small district, their restaurants will be in the venues list because they are enough close to another main district or neighborhood.

* List of venues (restaurants):

Though we specified **Restaurant** as the query for Foursquare API it returns some venues that are not really restaurants. We have to detect these cases and axclude them from the final list.

* Coordinates (GEO):

Some of the places are not geolocated. As we did with incorrect neighborhoods, we remove these places.
