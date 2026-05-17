# Actor - Idealista Scraper

## Idealista scraper

Since Idealista doesn't provide a public API, this actor retrieves property data from Idealista (Spain, Portugal, Italy).

### Features

-   **Scrape property details** ? price, size, rooms, bathrooms, photos, videos, 3D tours, contact info, and more.
-   **Scrape for-sale or rental properties** ? target sale or rent listings directly.
-   **Search by location** ? use a city or district name to search.
-   **Filter by URL** ? paste any Idealista search URL (with filters already applied) as a `startUrl`.
-   **Advanced filters** ? bedrooms, bathrooms, size range, home type, floor height, condition, and features.

> **Note:** Due to Idealista's privacy policy, exact property locations may be hidden. In those cases the scraper returns the map center coordinates accessible from the property detail.

## Input Parameters

| Field            | Type    | Required | Description |
|------------------|---------|----------|-------------|
| `country`        | String  | ?        | `es` (Spain), `pt` (Portugal), `it` (Italy) |
| `operation`      | String  | ?        | `sale` or `rent` |
| `proxy`          | Object  | ?        | Proxy configuration ? **RESIDENTIAL proxies required** |
| `district`       | String  |          | Location name to search, e.g. `Madrid`. Required if no `startUrl` provided. |
| `propertyType`   | String  |          | `homes` (default), `newDevelopments`, `bedrooms`, `offices`, `premises`, `transfers`, `garages`, `lands`, `storageRooms`, `buildings` |
| `startUrl`       | Array   |          | List of Idealista property detail or search URLs |
| `maxItems`       | Integer |          | Maximum number of results to return |
| `endPage`        | Integer |          | Last page number to scrape (default 50) |
| `minSize`        | String  |          | Minimum property size in m�, e.g. `"60"` |
| `maxSize`        | String  |          | Maximum property size in m�, e.g. `"200"` |
| `bedrooms`       | Array   |          | e.g. `["studio","1","2","3","4"]` |
| `bathrooms`      | Array   |          | e.g. `["1","2","3"]` |
| `homeType`       | Array   |          | `flat`, `penthouse`, `duplex`, `detachedHouse`, `semiDetachedHouse`, `terracedHouse`, `countryHouse`, `apartment`, `villa`, `loft` |
| `condition`      | Array   |          | `newDevelopment`, `good`, `renew` |
| `propertyStatus` | Array   |          | `bareOwnership`, `tenanted`, `illegallyOccupied`, `free` |
| `floorHeights`   | Array   |          | `topFloor`, `intermediateFloor`, `groundFloor` |
| `features`       | Array   |          | `airConditioning`, `builtinWardrobes`, `elevator`, `exteriorDomesticSpace`, `balcony`, `terrance`, `exterior`, `garage`, `garden`, `swimmingPool`, `storeRoom`, `accessible`, `luxury` |
| `onlyNewest`     | Boolean |          | Return only newest listings |
| `debugLog`       | Boolean |          | Enable verbose debug logging |

This solution requires **Proxy servers**. Use [Apify Proxy](https://www.apify.com/docs/proxy) with the **RESIDENTIAL** group or your own residential proxies.

## Example Result

```json
{
    "url": "https://www.idealista.com/obra-nueva/109497241/",
    "title": "Flat in calle Cantalejo, 19",
    "id": "109497241",
    "price": 629328,
    "size": 85,
    "baths": 2,
    "rooms": 2,
    "address": "calle Cantalejo, 19",
    "hideAddress": true,
    "latitude": 40.4745112,
    "longitude": -3.7368474,
    "typology": "flat",
    "subTypology": null,
    "photos": [
        {
            "url": "https://img4.idealista.com/blur/480_360_mq/0/id.pro.es.image.master/a9/f6/68/1356345714.webp",
            "tag": "facade",
            "localizedName": "Facade",
            "deeplinkUrl": null
        }
    ],
    "videos": [],
    "3dtour": [],
    "listingUpdate": "2024-03-15T10:00:00.000Z",
    "listingUpdateText": "Updated 2 days ago",
    "priceDown": null,
    "priceDownPercentage": null,
    "contacts": {
        "commercialName": "Grupo Ibosa",
        "contactName": "NR Village homes",
        "phone1": {
            "phoneNumber": "919388896",
            "formattedPhone": "919 38 88 96",
            "prefix": "34",
            "phoneNumberForMobileDialing": "+34919388896",
            "nationalNumber": true,
            "formattedPhoneWithPrefix": "+34 919 38 88 96"
        }
    }
}
```

##### Tip

To use a filtered search: go to Idealista, apply filters on the search page, then copy and paste the URL as a `startUrl` entry.

## Bugs, fixes, updates and changelog

If you have any feature requests you can create an issue from [here](https://github.com/laster04/Idealista-scraper/issues).
[Here](https://github.com/laster04/Idealista-scraper/blob/main/CHANGELOG.md) is the changelog with new features and bugfix info.
