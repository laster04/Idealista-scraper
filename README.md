# Actor - Idealista Scraper

## Idealista scraper

Since Idealista doesn't provide an API this actor should help you to retrieve data from it.

The Idealista data scraper supports the following features:

-   Scrape property details - You can scrape attributes like property images, price, features, neighborhood, nearby schools and many more. You can find details below.

-   Scrape for sale properties - If you are looking for a property which is for sale, you can directly target them.

-   Scrape rental properties - Rental properties can be directly targeted.

-   Scrape by keyword - You can use location-wise keywords to search specific search lists. Also you can directly point out rental, for sale or sold properties on this feature.

-   Scrape properties by filter - Auto detection of URLs helps you to directly copy/paste the URLs into the scraper to apply any filtering you like.
-   This scraper works only for Spain and Portugal, if you need to scrape **Italy** please use [this actor](https://apify.com/lukass/idealista-crawler-italy)
-   Through the new policy of web the exact location of some properties is hidden. So the scraper now get center of map which is accessible from detail of property.

## Input Parameters

The input of this scraper should be JSON containing the list of pages on Realtor that should be visited. Required fields are:

| Field     | Type    | Description                                                                                                        |
|-----------|---------|--------------------------------------------------------------------------------------------------------------------|
| district  | String  | (optional) Keyword that can be searched in Realtor search engine. When it is present, `mode` must be used as well. |
| country   | String  | (required) Select country where your search would be.                                                              |
| maxItems  | Integer | (optional) You can limit scraped products. This should be useful when you search through the big subcategories.    |
| endPage   | Integer | (optional) Final number of page that you want to scrape. Default is `Infinite`. This option overrides maxItems.    |
| startUrls | Array   | (optional) List of Idealista URLs. You should only provide property detail or search URLs                          |
| proxy     | Object  | Proxy configuration                                                                                                |

This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy). Scraper works only with **RESIDENTIAL** proxies right now.

##### Tip

When you want to have a filtering over a search URL; go to Idealista, create filters over the serach list and copy and paste the link as one of the **startUrl**.

## Bugs, fixes, updates and changelog
If you have any feature requests you can create an issue from [here](https://github.com/laster04/Idealista-scraper/issues).
[Here](https://github.com/laster04/Idealista-scraper/blob/main/CHANGELOG.md) is changelog with new features and bugfixes info.
