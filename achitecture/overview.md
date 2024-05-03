# Overview

## Features

### I18n (Internationalization)

We use ISO 639-2:1998 alpha-3 language code (example: ukr, eng, deu, fra, etc) for identifications of languages.

Available languages:
- 1st round (base):
    - Ukrainian (ukr);
    - English (eng);
- 2nd round (primary European languages):
    - Standard High German (deu);
    - French (fra);
    - Spanish (spa);
    - Portuguese (por);
    - Italian (ita);
    - Dutch (nld);
- 3rd round (classic languages):
    - Latin (lat);
    - Ancient Greek (grc);
    - Hebrew (heb);
- 4th round (german & celtic languages):
    - Irish (gle);
    - Welsh (cym);
    - Breton (bre);
    - Cornish (cor);
    - Manx (glv);
    - Scottish Gaelic (gla);
    - Low German (nds);
    - Luxembourgish (ltz);
    - Danish (dan);
    - Swedish (swe);
    - Norwegian Bokmål (nob);
    - Norwegian Nynorsk (nno);
- 5th round (mediterranean languages):
    - Modern Greek (ell);
    - Catalan (cat);
    - Occitan (oci);
    - Albanian (sqi);
- 6th round (slavic languages+romanian+crimean tatar):
    - Polish (pol);
    - Czech (ces);
    - Slovak (slk);
    - Serbian (srp);
    - Croatian (hrv);
    - Bosnian (bos);
    - Bulgarian (bul);
    - Macedonian (mkd);
    - Slovene (slv);
    - Belarusian (bel);
    - Romanian (ron);
    - Crimean Tatar (crh);
- 7th round (baltic languages):
    - Latvian (lav);
    - Lithuanian (lit);
- 8th round (Finno-Ugric languages):
    - Estonian (est);
    - Finnish (fin);
    - Hungarian (hun);
- 9th round (other european languages):
    - Basque (eus);
    - Georgian (kat);
    - Armenian (hye);
- 10th round (primary asian languages):
    - Levantine Arabic (apc);
    - Bengali (ben);
    - Bhojpuri (bho);
    - Mandarin (cmn);
    - Gujarati (guj);
    - Hindi (hin);
    - Javanese (jav);
    - Japanese (jpn);
    - Korean (kor);
    - Marathi (mar);
    - Southern Min (nan);
    - Punjabi (pan);
    - Iranian Persian (pes);
    - Tamil (tam);
    - Telugu (tel);
    - Azerbaijani (aze);
    - Turkish (tur);
    - Urdu (urd);
    - Vietnamese (vie);
    - Wu (wuu);
    - Yue (yue);
- 12th round (primary african languages):
    - Egyptian Arabic (arz);
    - Hausa (hau);
    - Swahili (swa);

### Authorization

#### By handle_name and password

#### ❓ By centralized authorization provider

##### ❓ Auth0

##### ❓ Firebase Auth

##### ❓ Clerk

##### ❓ KeyCloak

##### ❓ Cognito

##### ❓ SuperTokens

##### ❓ Nhost

##### ❓ By Google

##### ❓ By Facebook

#### Changing password

### Profile

- handle_name (human readable identifier of an account):
    - minimal length: 3
    - maximal length: 50
    - allowed symbols: A-Z,a-z,1-9,_.-,+,$
    - it must be unique in whole system
- Full name (max 50 symbols);
- Email address(es);
- Phone number(s);
- Avatar image (Size 400x400px	Max upload size of 2Mb. Supports PNG, GIF or JPEG);
- Header image (Size 1500x500px	Max upload size of 5Mb. Supports PNG or JPEG);
- Bio (max 1024 symbols);
- Country(ies);
- Language(s);
- Settings:
    - Permissions:
        - Read profile information;
        - Read posts;
        - Comment posts;
        - React on posts;
        - Read quick-posts;
        - Comment quick-posts;
        - React on quick-posts;
    - Notifications:

#### ❗(Un)Following mechanics

### ❗Content creating

#### Series

It is some kind of labeling of content entities to categorize it.
For example you can create seria `Rome` and add qposts, posts, albums with adding label of this seria. Then you can go to tab of series, pick `Rome` seria and consume the content of this seria.

#### ❗Image-based posts (albums)

#### ❗Short form content (stories/reels)

#### ❓ Short-Form Videos

#### ❓❓ Long-Form Videos

#### ❓❓ Live Streams

#### ❗Polls & Questions

#### Micro blogging

It should similar to tweets in twitter. It is called `quick-post (qpost)` in this social network.
You can attach media file to a qpost.
Limits:

- text (limit: max 300 symbols);
- medias:
    - number (max: 10 images);
    - images:
        - dimensions (1024x512px);
        - size (max upload size of 5Mb (or 3Mb for animated GIFs));
        - extensions (supports PNG, GIF or JPEG);
    - videos:
        - size (max upload size of 512MB);
        - length (Max length of video uploads	2'20" (140 seconds));
        - extensions (supports MP4 video format with H264 format with AAC audio);

The service supports commenting qposts and reacting on qposts.

#### Macro blogging

Limits:

- text (limit: max 65000 symbols);
- medias:
    - number (max: 80 images);
    - images
        - dimensions 1024x512px;
        - size (max upload size of 5Mb (or 3Mb for animated GIFs));
        - extensions (supports PNG, GIF or JPEG);
    - videos:
        - size (max upload size of 512MB);
        - length (Max length of video uploads	2'20" (140 seconds));
        - extensions (supports MP4 video format with H264 format with AAC audio);

#### ❗Channels


#### ❓ Articles

It is similar to pages in wikipedia.
But it should have versioning system not based on language like in wikipedia.
But it is based on authority (you can edit articles that you created and the articles that the owner allowed you to edit it).
But you can fork any article you have at least read-only access to.

#### Offerings

It looks like album content type but it includes price and initial currency.
This type of content dedicated for internet shops but without payment. It just makes easy to use this service as an ecommerce platform.
Besides, it allows for sales to set prices & description easier than it is for other content type records.

### ❗Messages

Features:

- scheduled messages;
- send message when addressant is online;
- reactions on messages;
- share geolocation:
    - selected location;
    - live location;
- voice messages;
- video messages;

#### ❗Direct messages

#### ❗Anonymous chats

#### ❗Group messages

Features:

- pools in message groups;

### Groups

It is place of communication of a community.
It has topics like in a forum where a participants can discuss on selected topic.
Groups must be portable like accounts are.

Features:

- internal content (qposts, posts, albums, pools, etc);
- topics;
- custom roles based on list of basic roles;

## Decisions

### ID generation

The best fit for the social network ID is numeric ID.
In order to achieve consistency we need to guarantee that IDs would not be repeated in different services because a data is portable in the scope of the network.
So, [SnowflakeID](https://en.wikipedia.org/wiki/Snowflake_ID) looks like great fit for this purpose.

It has golang implementation [github.com/bwmarrin/snowflake](https://pkg.go.dev/github.com/bwmarrin/snowflake@v0.3.0).
Ir requires node (int64). But it must be in range between 0 and 1023.

```go
node := 
n, err := snowflake.NewNode(node)
if err != nil {
    return nil, err
}
```

Each node in PDS's network would have twin seed source:
- zookeeper seed;
- PDS own seed;

For example:
We have:
- Zookeeper1 (seed=1):
    - PDS1 (seed=1); => resultingSeed(1, 1)
    - PDS2 (seed=2); => resultingSeed(1, 2)
    - PDS3 (seed=3); => resultingSeed(1, 3)
- Zookeeper2 (seed=2):
    - PDS1 (seed=1); => resultingSeed(2, 1)

Besides, each PDS store ID that was created by it and never generate this ID again.
Keep in mind that an accounts are portable and the account that was created in the PDS could be transferred to some another PDS.

### 2 factor Authorization

It is important to provide 2 factor authorization for users.
Email addresses and phone numbers should help with it.

### We must guarantee idempotency for all our endpoint

Best option for it is using `X-Idempotency-Key` header for all not idemponent operations (`POST` requests).
Client will generate unique string each time for each request. Then the server save all these keys for 24h and if some request uses the same `X-Idempotency-Key` the system raises the error that it is duplicated request.

When a client submits a duplicate idempotency key, we should return 409 CONFLICT.

### Formats

#### Datetime format

Use strings for timestamps, not numbers like milliseconds-since-epoch. Human readability matters! Someone glancing at "2023-12-21T11:17:12.34Z" might notice that it's a month in the future; someone glancing at 1703157432340 will not.

There is a [standard format](https://en.wikipedia.org/wiki/ISO_8601) for timestamps. It looks like the string above (including the 'T'). All of your clients will have easy access to library routines that parse and generate this format.

All timestamps should be in UTC ("Z").

Bad arguments for numeric timestamps include:

- "There are multiple date/time formats" - Use ISO8601.
- "Adding/subtracting to UTC is hard" - It's easier than counting seconds since 1970.
- "Parsing numbers is faster" - If you care that much about performance, use a binary format rather than JSON.

I don't see it in golang `time` library, so we need to create custom one

```go
var format = "2006-01-02T15:04:05.999Z"
var timestamp = time.Now().UTC().Format(format)
```

#### Country code format

We use lowercased ISO 3166-1 alpha-3 country code.

Example: ukr, usa, deu, gbr, etc.


#### Language code format

We use lowercased ISO 639-2:1998 alpha-3 language code.

Example: ukr, eng, deu, fra, etc.

#### Currency code format

We use lowercased ISO 4217 currency code.

Example: usd, uah, eur, etc.

#### Geolocation

We store geolocation as a [longitude, latitude] where `longitude` is decimal and `latitude` is decimal.

### Use structured error format

We should fit [Problem Details for HTTP APIs specification](https://www.rfc-editor.org/rfc/rfc7807).
According to it error response must contain:

- `application/problem+json` media type;
- next fields:
    - "type" (string) - A URI reference [RFC3986](https://www.rfc-editor.org/rfc/rfc3986) that identifies the
      problem type.  This specification encourages that, when
      dereferenced, it provide human-readable documentation for the
      problem type (e.g., using HTML [W3C.REC-html5-20141028](https://www.rfc-editor.org/rfc/rfc7807#ref-W3C.REC-html5-20141028)).  When
      this member is not present, its value is assumed to be
      "about:blank".
    - "title" (string) - A short, human-readable summary of the problem
      type.  It SHOULD NOT change from occurrence to occurrence of the
      problem, except for purposes of localization (e.g., using
      proactive content negotiation; see [RFC7231, Section 3.4](https://www.rfc-editor.org/rfc/rfc7231#section-3.4)).
    - "status" (number) - The HTTP status code ([RFC7231, Section 6](https://www.rfc-editor.org/rfc/rfc7231#section-6))
      generated by the origin server for this occurrence of the problem.
    - "detail" (string) - A human-readable explanation specific to this
      occurrence of the problem.
    - "instance" (string) - A URI reference that identifies the specific
      occurrence of the problem.  It may or may not yield further
      information if dereferenced.

Additionally we need to have some custom fields:

- validation errors/missing resource error/ etc (`errors`);
- error's identifier (`logref`, use `nano ID generator` (length: 12));

Example of REST API JSON response:
```json
{
    "type": "about:blank",
    "title": "Bad Request",
    "status": 400,
    "detail": "ValidationError",
    "instance": "/books/1",
    "errors": [
        {
            "field": "name",
            "reason": "missing"
        }
    ],
    "logref": "yhd_Nd3ZRunN"
}
```

### REST API conventions

We try to follow RESTful API best practices:

- name of a resource — a plural noun
- action on a resource — HTTP method that use user of the application:
    - `GET` — get a resource;
    - `POST` — create a resource;
    - `PUT` — modify a resource fully (refresh it);
    - `DELETE` — delete a resource;
    - `PATCH` — modify a resource particularly;
    - `COPY` — making a resource copy;

But sometimes we need to go out from these limits because of some technical limitations like length of URL.

#### Search endpoints

So, we use `POST` HTTP method for making request for doing search. We will use a lot of filters there and in order to not change HTTP method in future we use `POST` method there from the start.

#### Running commands

We use `POST` HTTP method for endpoints where we need to run command like: validate, run, send, etc.
Why? Because it is creation in some sense too. As well as we create validation, sending, etc.

### Header conventions

We need to use custom fields for request/response headers. For gRPC requests/responses we do it in its way.

#### `X-Request-Id`

If it's used in request it sets request ID for the request and you will see the same request ID in response's header.
If it isn't set in request's headers it will be generated (use `nano ID generator` (length: 12)) automatically but a server and you will see it in response's header.
Besides, it's used for writing down all logs related to each request.

#### `X-App-Version`

It is [semver version](https://semver.org/) of responding server.

#### `X-Timestamp`

It is timestamp generated just before sending a response. This timestamp as other datetime values follows ISO8601 format.

#### `X-Duration`

It is duration of a request's processing in Milliseconds (ms).
