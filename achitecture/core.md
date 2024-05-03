# Core

It is the only centralized part of the application.

## Components

### ❗Geo Service

It is golang gRPC server. It is dedicated for doing all centralized geolocation stuff here:

- searching locations by coordinates, address, or raw name;
- adding check ins for places;
- adding reviews for places;


We can use [OpenStreetMap Nominatim](https://nominatim.org/release-docs/develop/api/Overview/) or [Google Maps Geocoding API](https://github.com/googlemaps/google-maps-services-go) as geocoding service.

Arango DB provides fuzzy search ([link](https://docs.arangodb.com/3.10/index-and-search/arangosearch/fuzzy-search/#fuzzy-search-in-arangodb)).
Besides, Arango DB supports geo data storing ([link](https://docs.arangodb.com/3.10/aql/functions/geo/)).

Stages of location search:

1. Geocoding (the address is first converted into geographic coordinates (latitude and longitude))
2. Address Standardization (before matching the input address with our database's addresses, we apply address standardization techniques to normalize the address format. This helps ensure consistency and improves the accuracy of address matching. Standardization may involve removing punctuation, converting abbreviations to full words, and formatting the address according to a predefined schema)
3. Fuzzy Matching (we use fuzzy matching algorithms to compare it with the addresses in their database. Fuzzy matching allows for approximate string matching, taking into account variations in spelling, punctuation, and formatting. This helps to identify potential matches even when there are minor differences between the input address and the addresses stored in the database)
4. Scoring and Ranking (it assigns scores or rankings to each match based on various factors such as proximity, relevance, and confidence level. Matches with higher scores or rankings are more likely to be considered accurate and relevant to the input address)
5. Verification and Validation (we may incorporate user feedback, crowdsourced data, or manual verification processes to validate the accuracy of address matches and improve the quality of their database. Users may be prompted to confirm or correct the matched address, helping to refine the matching algorithms over time)

#### ❗Endpoints

#### Entities

##### Place

| Field name          | Type                                                               |
|---------------------|--------------------------------------------------------------------|
| *id                 | numeric string                                                     |
| *created_at         | datetime                                                           |
| *location           | [longitude, latitude]                                              |
| *name               | string                                                             |
| *name_language      | language code string                                               |
| *category           | `enum Category`                                                    |
| *address            | string                                                             |
| phone_number        | string                                                             |
| website             | URL string                                                         |
| hours               | `object Hours`                                                     |
| rating              | number                                                             |
| total_check_ins     | number                                                             |
| images_urls         | array of URL strings                                               |

```ts
enum Category {
    Restaurant,
    Cafe,
    Park,
    Church,
}
```

```ts
interface Hours {
    sunday: {open: string, close: string}
    monday: {open: string, close: string}
    tuesday: {open: string, close: string}
    wednesday: {open: string, close: string}
    thursday: {open: string, close: string}
    friday: {open: string, close: string}
    saturday: {open: string, close: string}
}
```

##### Check In

| Field name          | Type                                                               |
|---------------------|--------------------------------------------------------------------|
| *id                 | numeric string                                                     |
| *created_at         | datetime                                                           |
| *account_id         | numeric string                                                     |
| *place_id           | numeric string                                                     |
| *image_url          | URL string                                                         |

##### Review

| Field name          | Type                                                               |
|---------------------|--------------------------------------------------------------------|
| *id                 | numeric string                                                     |
| *created_at         | datetime                                                           |
| *account_id         | numeric string                                                     |
| *place_id           | numeric string                                                     |
| *rating             | number                                                             |
| *comment            | string                                                             |
| *comment_language   | language code string                                               |


#### Technology stack:

Programming language: golang

Transport: gRPC

Databases: arangodb, redis

### ❗Payments service

It is golang gRPC(❓) server.

#### ❗Endpoints

#### ❗Entities

#### Technology stack:

Programming language: golang

Transport: gRPC

Databases:

### ❗Plugin Store

It is golang gRPC server.

Possible plugins:
- personalized GPT assistant (voiced);
- writing texts assistant;

#### ❗Endpoints

#### ❗Entities

#### Technology stack:

Programming language: golang

Transport: gRPC

Databases:

### ❗Zookeepers Manager

It is golang gRPC server. It is dedicated for storing plugins and customers of it.
Besides, for some plugins it is okay to use resources of user's machine. So, it is reason why it is reasonable to build client apps:
- iOS mobile app
- android mobile app
- windows desktop app
- linux desktop app
- macOS desktop app

#### ❗Endpoints

#### ❗Entities

#### Technology stack:

Programming language: golang

Transport: gRPC

Databases:

### ❗iOS application

### ❗Android application

### ❗Windows desktop application

### ❗Linux desktop application

### ❗MacOS desktop application

## Decisions
