# Orbis Socialis (Social World)

It is cluster of services that provides feed of quick-posts, existing and functionality of groups, moderation of data.
Besides, here is stored public (not private, and not personal stored at user's personal page) posts and quick-posts.

## Components

### Crawler

Worker that works rather like an actor than like HTTP server.
This service should be written in golang. Use gRPC in needs.

#### Description

It serves for crawl records from other Orbis Socialis clusters.
Besides, this service keep actual accounts information by requesting PDSs of residents of this Orbis Socialis.

### Ingress Service

Golang gRPC  server for writing commands.

#### Description

It is one of key services of the Orbis Socialis. It holds all main functionality only WRITING functionality for core data (NOT PERSONAL) of the application.

#### Endpoints

- accounts:
    - attaching an account to the Orbis Socialis service
    - disattaching an account from the Orbis Socialis service
    - transfering an account from one Orbis Socialis service to another one
- posts:
    - endpoint for creation of record of publisher's post;
    - endpoint for deleting of record of publisher's post;
- quick-posts:
    - endpoint for creation of record of publisher's quick-post;
    - endpoint for deleting of record of publisher's quick-post;
- groups:
    - endpoint for creation a group
    - endpoint for updating a group information
    - endpoint for deleting a group
    - endpoint for creating a group post
    - endpoint for updating a group post
    - endpoint for deleting a group post
    - endpoint for creating a group comments under group post
    - endpoint for updating a group comments under group post
    - endpoint for deleting a group comments under group post
    - endpoint for creating a reactions under group post
    - endpoint for updating a reactions under group post
    - endpoint for deleting a reactions under group post
    - forums:
        - endpoint for creation a group forum topic
        - endpoint for updating a group forum topic
        - endpoint for deleting a group forum topic
        - endpoint for creation a group forum topics's record
        - endpoint for updating a group forum topics's record
        - endpoint for deleting a group forum topics's record
        - endpoint for creation a group album
        - endpoint for updating a group information
        - endpoint for deleting a group album
        - endpoint for uploading media to a group album. Available media formats:
            - image (PNG, GIF or JPEG)
            - video (MP4 video format with H264 format with AAC audio)
        - endpoint for updating an information about group album's media
        - endpoint for deleting media from a group album

### API Gateway

Golang REST API server for retrieving data by queries and act as proxy for writing commands.

#### Description

It is one of key services of the Orbis Socialis. It holds all main functionality only READING functionality for core data (NOT PERSONAL) of the application.

#### Endpoints

- search (single endpoint):
    - filters:
        - by type
        - by account's `handle_name`
        - by text (postgres `LIKE` would be used)
        - by Orbis Socialis
    - types of entities:
        - for posts
        - for quick-posts
        - groups
- posts:
    - endpoint for retrieving single post with comments and reactions (1st page of pagination + total number)
    - endpoint for retrieving the account's posts
    - endpoint for retrieving posts as a feed
    - endpoints for retrieving the post's comments
    - endpoints for retrieving the post's reactions
- public quick-posts:
    - endpoint for retrieving single quick-post with comments and reactions (1st page of pagination + total number)
    - endpoint for retrieving the account's quick-posts
    - endpoint for retrieving quick-posts as a feed
    - endpoints for retrieving the quick-post's comments (pagination)
    - endpoints for retrieving the quick-post's reactions (pagination)
- groups:
    - endpoint for retrieving the account's groups
    - endpoint for retrieving the group's information
    - endpoint for retrieving the group's topics
    - endpoint for retrieving the group's topic's records
    - endpoint for retrieving the group's albums
    - endpoint for retrieving the group's album's medias

### Admin

SSR frontend application with REST API endpoints.
NextJS is good technology for this service.

#### Description

The service provides functionality for configuring the Orbis Socialis and for setting moderation rules, and tools for doing the moderation.
