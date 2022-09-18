# Actor - Idealista Scraper

## Idealista scraper

Since Idealista doesn't provide an API this actor should help you to retrieve data from it.

The Idealista data scraper supports the following features:

-   Scrape property details - You can scrape attributes like property images, price, features, neighborhood, nearby schools and many more. You can find details below.

-   Scrape sold properties - You can scrape sold properties through a search list.

-   Scrape for sale properties - If you are looking for a property which is for sale, you can directly target them.

-   Scrape rental properties - Rental properties can be directly targeted.

-   Scrape by keyword - You can use location-wise keywords to search specific search lists. Also you can directly point out rental, for sale or sold properties on this feature.

-   Scrape properties by filter - Auto detection of URLs helps you to directly copy/paste the URLs into the scraper to apply any filtering you like.

## Input Parameters

The input of this scraper should be JSON containing the list of pages on Realtor that should be visited. Required fields are:

| Field                | Type    | Description                                                                                                                                                                                               |
| -------------------- | ------- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| startUrls            | Array   | (optional) List of Idealista URLs. You should only provide property detail or search URLs                                                                                                                 |
| maxItems             | Integer | (optional) You can limit scraped products. This should be useful when you search through the big subcategories.                                                                                           |
| endPage              | Integer | (optional) Final number of page that you want to scrape. Default is `Infinite`.                                                                                                                           |
| search               | String  | (optional) Keyword that can be searched in Realtor search engine. When it is present, `mode` must be used as well.                                                                                        |
| mode                 | String  | (optional) Mode of the actor. It gets the keyword from `search` parameter and initiate the search according to the mode. Can be `BUY`, `RENT` or `SOLD`. When present, `search` must be provided as well. |
| extendOutputFunction | String  | (optional) Function that takes a JQuery handle ($) as argument and returns object with data                                                                                                               |
| proxy                | Object  | Proxy configuration                                                                                                                                                                                       |

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

##### Tip

When you want to have a filtering over a search URL; go to Idealista, create filters over the serach list and copy and paste the link as one of the **startUrl**.

### Compute Unit Consumption

The actor optimized to run blazing fast and scrape many as properties as possible. Therefore, it forefronts all property detail requests. If actor doesn't block very often it'll scrape 50 properties in 2 minutes with ~0.05-0.07 compute units.


## Bugs, fixes, updates and changelog
If you have any feature requests you can create an issue from [here](https://github.com/laster04/Idealista-scraper/issues).
[Here](https://github.com/laster04/Idealista-scraper/blob/main/CHANGELOG.md) is changelog with new features and bugfixes info.
