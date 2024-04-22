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
- 8th round (finno-hungerian languages):
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

#### Changing password

### Profile

- handle_name (human readable identifier of an account):
    - minimal length: 3
    - maximal legnth: 50
    - allowed symbols: A-Z,a-z,1-9,_.-,+,$
    - it must be unique in whole system
- Full name (max 50 symbols);
- Email address(es);
- Phone number(s);
- Avatar image (Size 400x400px	Max upload size of 2Mb. Supports PNG, GIF or JPEG);
- Header image (Size	1500x500px	Max upload size of 5Mb. Supports PNG or JPEG);
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

#### (Un)Following mechanics

### quick-post (the same as tweet in twitter) posting

It can contain:
- text (limit: max 300 symbols);
- image (Size 1024x512px	Max upload size of 5Mb (or 3Mb for animated GIFs). Supports PNG, GIF or JPEG);
- video (Max length of video uploads	2'20" (140 seconds)	MP4 video format with H264 format with AAC audio. Max upload of 512MB);

#### Commenting of quick-posts

### Feed of quick-posts

### Posting posts on own page

It can contain:
- text (limit: max 65000 symbols);
- images
    - Size 1024x512px;
    - Max upload size of 5Mb (or 3Mb for animated GIFs);
    - Supports PNG, GIF or JPEG;
    - Max number of images per post is 80;
- video (Max length of video uploads	2'20" (140 seconds)	MP4 video format with H264 format with AAC audio. Max upload of 512MB);

#### Commenting of posts

### Messaging

#### Direct messages

#### Group messages

### Groups
It is like facebook or vkontakte groups

#### Internal posts

##### Commenting of internal posts

#### Forum with topics

#### Gallery

It contains group's albums.

### Articles

It is similar to pages in wikipedia.
But it should have versioning system not based on language like in wikipedia.
But it is based on authority (you can edit articles that you created and the articles that the owner allowed you to edit it).
But you can fork any article you have at least read-only access to.
