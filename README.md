# Actor - Idealista Scraper

## Idealista scraper

Since Idealista doesn't provide a public API, this actor retrieves property data from Idealista (Spain, Portugal, Italy).

### Features

-   **Scrape property details** ? price, price per m�, size, floor, rooms, bathrooms, description, energy certification, lift/parking/feature flags, location breakdown (district, municipality, province, neighborhood), photos, videos, 3D tours, contact info, and more.
-   **Scrape for-sale or rental properties** ? target sale or rent listings directly.
-   **Search by location** ? use a city or district name to search.
-   **Filter by URL** ? paste any Idealista search URL (with filters already applied) as a `startUrl`.
-   **Advanced filters** ? bedrooms, bathrooms, size range, home type, floor height, condition, and features.

> **Note:** Due to Idealista's privacy policy, exact property locations may be hidden. In those cases the scraper returns the map center coordinates accessible from the property detail.

> **Note:** `description` is returned in the language the advertiser wrote it in (usually Spanish), even though titles and other labels come back in English.

## Pricing

This Actor uses **pay-per-event** billing ? you are not charged for Apify platform usage (compute, proxy bandwidth), only for the results you get.

| Event | Price | When it's charged |
|-------|-------|-------------------|
| `list-result` | $1.00 / 1,000 results | One per property returned from a search (`district` or a search `startUrl`) with `fetchDetails` disabled |
| `detail-result` | $3.50 / 1,000 results | One per property fetched from its detail page ? every result when `fetchDetails` is enabled, plus any direct property `startUrl` |

Each property is charged **once**: with `fetchDetails: true` search results are not pushed on their own, so you pay `detail-result` only ? never both events for the same property.

Detail results cost more because each one needs its own extra API request through residential proxies, on top of the search request. If you only need the fields listed in the search response (see the note under [Example Result](#example-result)), leave `fetchDetails` off and pay the `list-result` rate.

Use `maxItems` to cap how many results ? and therefore how much ? a run can produce.

## Input Parameters

| Field            | Type    | Required | Description |
|------------------|---------|----------|-------------|
| `country`        | String  | ?        | `es` (Spain), `pt` (Portugal), `it` (Italy) |
| `operation`      | String  | ?        | `sale` or `rent` |
| `proxy`          | Object  | ?        | Proxy configuration ? **RESIDENTIAL proxies required** |
| `district`       | String  |          | Location name to search, e.g. `Madrid`. Required if no `startUrl` provided. |
| `propertyType`   | String  |          | `homes` (default), `newDevelopments`, `bedrooms`, `offices`, `premises`, `transfers`, `garages`, `lands`, `storageRooms`, `buildings` |
| `startUrl`       | Array   |          | List of Idealista property detail or search URLs, including drawn-area URLs (`/areas/...?shape=...`) |
| `maxItems`       | Integer |          | Maximum number of results to return |
| `endPage`        | Integer |          | Last page number to scrape (default 50) |
| `fetchDetails`   | Boolean |          | For each search result, also fetch the full property detail page (adds `description`, `energyCertification`, and more accurate `floor`/`hasLift`/location fields). Slower, uses one extra request per property, and bills at the `detail-result` rate (see [Pricing](#pricing)). Default `false`. |
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
    "url": "https://www.idealista.it/immobile/35994897/",
    "title": "Flat / apartment in Via della Balduina, 63, Centro di Balduina, Roma",
    "id": "35994897",
    "price": 830000,
    "size": 220,
    "priceByArea": 3773,
    "baths": 3,
    "rooms": 10,
    "address": "Flat / apartment in Via della Balduina, 63, Centro di Balduina, Roma",
    "hideAddress": false,
    "latitude": 41.9166671,
    "longitude": 12.4417612,
    "typology": "flat",
    "subTypology": null,
    "description": "BALDUINA | Refined 210 sq m apartment with livable terraces, garage, and cellar...",
    "energyCertification": null,
    "floor": "3",
    "status": "good",
    "newDevelopment": false,
    "hasLift": true,
    "externalReference": null,
    "district": "Balduina",
    "municipality": "Roma",
    "province": "Roma",
    "neighborhood": "Centro di Balduina",
    "locationId": "0-EU-IT-RM-01-001-097-38-002",
    "parkingSpace": {
        "hasParkingSpace": true,
        "isParkingSpaceIncludedInPrice": true
    },
    "features": {
        "hasSwimmingPool": false,
        "hasTerrace": false,
        "hasAirConditioning": true,
        "hasBoxRoom": true,
        "hasGarden": false
    },
    "labels": [
        { "name": "bright", "text": "Bright" }
    ],
    "highlight": "Top",
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

> **Note:** By default, search results (`district` or search-URL scraping) return the data included directly in the search response ? it does **not** include everything a single property page has. Enable `fetchDetails` to fetch the full detail page for every search result instead:
>
> - **`energyCertification`** is *only* available from the detail page ? there's no way to get it from search results, `fetchDetails` or not.
> - **`description`**, `size`, and `priceByArea` are present in both search results and detail pages.
> - **`neighborhood`**, `parkingSpace`, `newDevelopment`, and `highlight` are only present in search results ? they're not returned by the detail endpoint at all, so scraping via a direct property URL (`/inmueble/`, `/immobile/`, `/imovel/`) or with `fetchDetails` enabled won't populate them.
> - **`district`/`municipality`/`province`** use a different, coarser location breakdown on the detail page (it's approximated from Idealista's `administrativeAreaLevel1-3` fields, which don't line up cleanly with the search response's own district/municipality/province).
> - **`features`** (pool, terrace, air conditioning, etc.) is less complete from the detail page ? some flags (terrace, air conditioning) only exist there as free-text, not structured fields, so they're left out to avoid unreliable text-matching.

##### Tip

To use a filtered search: go to Idealista, apply filters on the search page, then copy and paste the URL as a `startUrl` entry.

Drawn-area searches work too: draw the area on Idealista's map, then paste the resulting `/areas/...?shape=...` URL as a `startUrl`. The polygon is used as the search area, so no district name is needed.

Filters in the URL path (price, size, rooms, bathrooms, home type, condition, features) are applied to the search and override the same fields in the actor input. Two caveats: the chalet subtypes (`chalets-independientes`, `chalets-adosados`, `casas-de-pueblo`, ...) are searched as one "houses" bucket, because the API has no subtype filter; and any filter token that cannot be mapped is logged as a warning and ignored.

## Bugs, fixes, updates and changelog

If you have any feature requests you can create an issue from [here](https://github.com/laster04/Idealista-scraper/issues).
[Here](https://github.com/laster04/Idealista-scraper/blob/main/CHANGELOG.md) is the changelog with new features and bugfix info.
