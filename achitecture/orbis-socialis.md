# Orbis Socialis (Social World)

It is cluster of services that provides feed of quick posts, existing and functionality of groups, moderation of data.
Besides, here is stored public (not private, and not personal stored at user's personal page) posts and quick posts.

## Components

### BFF (Backend for Frontend)

SSR frontend application with REST API endpoints.

#### Description

It serves as gateway (REST API) and as server that serves Browser Frontend.
This service works like proxy for WRITE commands and it can interact with database directly for READ queries.
The service interacting with PDSs for CRUD sessions, retrieving account data for user.

#### Endpoints

- search:
    - endpoint for search posts/quick posts/groups/accounts with filter
- feed:
    - endpoint for getting feed
- authorization:
    - endpoint for creating a session;
    - endpoint for refreshing a session;
    - endpoint for closing a session;
    - endpoint for getting account data;

### Crawler

Worker that works rather like an actor than like HTTP server.

#### Description

It serves for crawl records from other Orbis Socialis clusters.
Besides, this service keep actual accounts information by requesting PDSs of residents of this Orbis Socialis.

### Core

REST API server.

#### Description

It is main service of the Orbis Socialis. It holds all main functionality and it only has WRITE functionality for core data of the application.

#### Endpoints

- posts:
    - endpoints for CRUD posts
    - endpoints for CRUD comments under posts
    - endpoints for Create/Update/Delete reactions under posts
- public quick posts:
    - endpoints for CRUD public quick posts
    - endpoints for CRUD comments under public quick posts
    - endpoints for Create/Update/Delete reactions under public quick posts
- groups:
    - endpoints for CRUD groups
    - endpoints for CRUD group posts
    - endpoints for CRUD comments under group posts
    - endpoints for Create/Update/Delete reactions under group posts
    - forums:
        - endpoints for CRUD group forum topics
        - endpoints for CRUD group forum topics's records
        - endpoints for CRUD group albums
        - endpoints for CRUD group albums medias (images (PNG, GIF or JPEG), videos (MP4 video format with H264 format with AAC audio))

### Admin

SSR frontend application with REST API endpoints.

#### Description

The service provides functionality for configuring the Orbis Socialis and for setting moderation rules, and tools for doing the moderation.