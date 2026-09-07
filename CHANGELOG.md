
# Changelog

## [0.0.73] - 2026-09-07

### Major changes

- Rewritten to scrape Idealista's mobile API instead of the website HTML. Faster, far fewer blocks, and richer data (energy certification, features, agency info) on every result.
- **Pay-per-event pricing.** You are no longer billed for platform usage (compute, proxy bandwidth) ? only for results:
    - `list-result` ? $1.00 / 1,000 results (properties returned from a search)
    - `detail-result` ? $3.50 / 1,000 results (properties fetched from their detail page)
    - Each property is charged once ? with `fetchDetails` enabled you pay `detail-result` only, never both.
- New **`fetchDetails`** input. Fetches the full detail page for every search result ? adds `description`, `energyCertification` and more accurate `floor`/`hasLift`/location fields, at one extra request per property.
- **Drawn-area start URLs** supported. Draw an area on Idealista's map and paste the `/areas/...?shape=...` URL as a `startUrl`; the polygon is used as the search area, so no district name is needed.
- **URL path filters** (price, size, rooms, bathrooms, home type, condition, features) are parsed from `startUrl` and applied to the search, overriding the same fields in the actor input. Chalet subtypes are searched as one "houses" bucket (the API has no subtype filter); unmappable filter tokens are logged as a warning and ignored.
- Added filter inputs: `minSize`, `maxSize`, `bedrooms`, `bathrooms`, `preservations`, `features` and more ? see the README input table.
- Added dataset and output schemas, so results get a proper Overview table and typed fields on the platform.

### Fixes

- `url` is now always present in the output. Detail-page results had no listing URL ? it is rebuilt from the property id per country (`/inmueble/`, `/imovel/`, `/immobile/`).
- `hideAddress` now means the same thing in both search and detail results (the search response's inverted `showAddress` was being passed through as-is).
- `description` and other localized fields now respect the country of the run.
- Retry the OAuth token request on a fresh proxy IP (up to 5 attempts) instead of failing the whole run when Idealista's edge answers with 503.
- Fixed `406` responses caused by missing/incorrect request headers.
- Fixed URL encoding for locations with spaces and accents.
- Switched to `BasicCrawler`; updated Apify SDK and Crawlee.


## [0.0.66] - 2024-05-09

All notable changes to this project will be documented in this file.
## [0.0.48] - 2024-05-09

### Major changes

- SDK update
## [0.0.42] - 2024-05-09

### Major changes

- add Italy
## [0.0.41] - 2024-05-07

### Major changes

- update actor to V3 crawlee
## [0.0.37] - 2023-08-06

### Major changes

- Fix latitude and longitude because of advertisers privacy so now latitude and longitude should be center of map what's shows from property detail
## [0.0.36] - 2023-12-10

### Major changes

- Add rooms to output
## [0.0.33] - 2023-08-06

### Major changes

- Add other country PT
- ## [0.0.30] - 2023-08-06

### Major changes

- Add pagination to shape listing
## [0.0.25] - 2023-05-09

### Major changes

- Readme.md

## [0.0.24] - 2023-04-24

### Major changes

- add some params

## [0.0.23] - 2023-04-24

### Major changes

- add tags

## [0.0.22] - 2023-04-19

### Major changes

- add energy labels to output
- add other lang mutation

## [0.0.19] - 2023-04-12

### Major changes

- fix m2 over 1k

## [0.0.18] - 2023-03-27

### Major changes

- fix offline properties ads

## [0.0.17] - 2023-03-23

### Major changes

- add title to output, fix pagination, fix ubicationAddress
- fix enqueuing page urls
## [0.0.15] - 2023-03-14

### Major changes

- add typology of property to output
## [0.0.13] - 2023-03-01

### Major changes

- **MaxItems** settings.
    - Now max items per listing page.
- Add additionalLink and ubicationAddress

## [0.0.12] - 2023-03-01

### Major changes

- **EndPages** settings.
    - Now you can set max pages per listing url. This overrides maxItems settings.
## [0.0.9] - 2022-12-12

### Major changes

- Browse across sub locations on maps page.

## [0.0.8] - 2022-11-07

### Major changes

- Fix INPUT param name.

## [0.0.7] - 2022-11-02

### Major changes

- Fix maxItems input.
