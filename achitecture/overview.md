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

Features:

- internal content (qposts, posts, albums, pools, etc);
- topics;
- custom roles based on list of basic roles;

## Decisions

### ID generation

The best fit for the social network ID is numeric ID.
In order to achieve consistency we need to guarantee that IDs would not be repeated in different services because a data is portable in the scope of the network.
So, [SnowflakeID](https://en.wikipedia.org/wiki/Snowflake_ID) looks like great fit for this purpose 
