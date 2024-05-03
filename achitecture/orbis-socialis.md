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

#### Entities

#### Technology stack:

Programming language: golang

Transport: gRPC

Databases:

### Blockchain Peer

The service is golang gRPC server that serves as blockchain peer.

#### Description
The service dedicated for:
- storing of chains of actions with groups & channels (creation, deletation, transitions). It is sync with other Orbises Socialis;
- storing state of location all groups & channels (World State);

Good choice for storage is local instance of SQLite.
Use `MD6-256` as hash function.

When the service is starting up it calls zookeeper to get full list of Orbises Socialis.
After the service call validator Orbises Socialis from the list to get last transactions from shutting down timepoint.
Then transactions are applied and World State is updated.
After the service can process requests.

Validator is chosen by zookeeper. Beside, zookeeper should check status of all Orbises Socialis to choose validator by the best way for next time.
When the service call some other service and it doesn't response for 30s it should call zookeeper to report it. Then zookeeper do the request by itself and if it doesn't response it write this information to the register and this information will be considered next time when validator is choosing.

#### How the Blockchain works

It is a blockchain network for storing groups's & channels references.
The network should be synchronized inside of itself.
All peers should store full history of transactions.
Besides, it should also store "state of world". It is current state of data inside of the distributed ledger.

Structure of state of world entities:

```json
{
    "t": 0,
    "id": 1234567890,
    "oid": 3456789012
}
```

Where `t` = `entity type`, `id` = `entity's id`, `oid` = `orbis socialis id`.

```ts
enum EntityType {
    Group = 0,
    Channel = 1,
}
```

Transactions are operations with that objects.
Structure of a transaction should looks like:
```json
{
    "op": "create" | "transit" | "delete",
    "field": "aid" | "pid" | "oid",
    "value": "...." | null "{{t}}::{{id}}::{{oid}}",
    "identifier": "{{aid}}" | null
}
```

Structure of a block should looks like:
```json
{
    "header": {
        "hash": "9071d70b9e9440078e4ddf7d2cb19ffd4c04a04b75bbbfba9eae3216223ce9f2",
        "parent_block_hash": "9b90c5a68b78e1dbf215e66102df54f60855bfcd843318627f13cf84896a2a39",
        "timestamp": "1713871179828"
    },
    "data": {
        "op": "create",
        "field": null,
        "value": "0::1234567890::3456789012",
        "identifier": null
    }
}
```

#### Endpoints

- endpoint for getting service status (`GET/health`)
- endpoint for getting PDSs with statuses
- endpoint for creating transaction (`POST/txs`)
- endpoint for running validation in validator (`POST/validate`)
- endpoint for retrieving blocks after some block hash (`GET/blocks?from=9b90c5a68b78e1dbf215e66102df54f60855bfcd843318627f13cf84896a2a39`)
- endpoint for getting state of entities (`GET/entities?t=0&ids=1234567890,1234567891,1234567892`) it should works only with IDs (`ids`) and type (`t`).

#### Entities

#### Technology stack:

Programming language: golang

Transport: gRPC

Databases: SQLite

### Ingress Service

Golang gRPC  server for writing commands.

#### Description

It is one of key services of the Orbis Socialis. It holds all main functionality only WRITING functionality for core data (NOT PERSONAL) of the application.

#### Endpoints

- accounts:
    - attaching an account to the Orbis Socialis service
    - disattaching an account from the Orbis Socialis service
    - transferring an account from one Orbis Socialis service to another one
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

#### Entities

##### Group

| Field name         | Type                                                               |
|--------------------|--------------------------------------------------------------------|
| *id                | numeric string                                                     |
| *name              | string                                                             |
| *description       | string                                                             |
| *profile_image_url | URL string                                                         |
| *header_image_url  | URL string                                                         |
| *created_at        | datetime                                                           |
| last_modified_at   | datetime                                                           |
| privacy            | enum `GroupPrivacy`                                                |
| is_anonymous       | boolean                                                            |

```ts
enum GroupPrivacy {
    Public
    Private
}
```

##### Group Custom Role

| Field name         | Type                                                               |
|--------------------|--------------------------------------------------------------------|
| *id                | numeric string                                                     |
| *group_id          | numeric string                                                     |
| *role              | enum `BaseRole`                                                    |
| *name              | string                                                             |
| *priority          | integer                                                            |
| *created_at        | datetime                                                           |
| last_modified_at   | datetime                                                           |

```ts
enum BaseRole {
    Admin
    Moderator
    Member
    PendingMember
    Banned
}
```

##### Group Participant

| Field name            | Type                                                               |
|-----------------------|--------------------------------------------------------------------|
| *id                   | numeric string                                                     |
| *account_id           | numeric string                                                     |
| *group_id             | numeric string                                                     |
| *base_role            | `enum BaseRole`                                                    |
| *group_custom_role_id | numeric string                                                     |
| *joined_at            | datetime                                                           |
| last_modified_at      | datetime                                                           |

##### Topic

| Field name          | Type                                                               |
|---------------------|--------------------------------------------------------------------|
| *id                 | numeric string                                                     |
| *created_at         | datetime                                                           |
| last_modified_at    | datetime                                                           |
| *group_id           | numeric string                                                     |
| *creator_account_id | numeric string                                                     |
| *title              | string (max: 100 symbols)                                          |
| *profile_image_url  | URL string                                                         |

##### Topic Record

| Field name          | Type                                                               |
|---------------------|--------------------------------------------------------------------|
| *id                 | numeric string                                                     |
| *created_at         | datetime                                                           |
| last_modified_at    | datetime                                                           |
| *group_id           | numeric string                                                     |
| *creator_account_id | numeric string                                                     |
| *topic_id           | numeric string                                                     |
| *text_content       | string                                                             |
| *media_urls         | URL strings                                                        |

##### Channel

| Field name          | Type                                                               |
|---------------------|--------------------------------------------------------------------|
| *id                 | numeric string                                                     |
| *created_at         | datetime                                                           |
| last_modified_at    | datetime                                                           |
|

##### Media

| Field name         | Type                                                               |
|--------------------|--------------------------------------------------------------------|
| *id                | numeric string                                                     |
| *created_at        | datetime                                                           |
| last_modified_at   | datetime                                                           |
| creator_account_id | numeric string                                                     |

#### Technology stack:

Programming language: golang

Transport: gRPC

Databases:

### API Gateway

Golang REST API server for retrieving data by queries and act as proxy for writing commands.

#### Description

It is one of key services of the Orbis Socialis. It holds all main functionality only READING functionality for core data (NOT PERSONAL) of the application.

#### Endpoints

- endpoint for validation of invite code (`validateInviteCode`);
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
    - endpoint for retrieving the group's posts
    - endpoint for retrieving the group's topics
    - endpoint for retrieving the group's topic's records
    - endpoint for retrieving the group's albums
    - endpoint for retrieving the group's album's medias

#### Technology stack:

Programming language: golang

Transport: REST API

Databases:

### Admin

SSR frontend application with REST API endpoints.
NextJS is good technology for this service.

#### Description

The service provides functionality for configuring the Orbis Socialis and for setting moderation rules, and tools for doing the moderation.

#### Entities

##### Admin

| Field name                   | Type                            |
|------------------------------|---------------------------------|
| *id                          | numeric string                  |
| *email                       | email string                    |
| *password hash               | string                          |

#### Technology stack:

Programming language: golang

Transport: REST API+SSR

Databases:

## Decisions

### Storing of media files

Ecumenos, being a decentralized social networking platform, can have variations in how media files are stored based on the instance's configuration and hosting setup.
However, the default behavior and common practice for our instances is to store media files on the local filesystem of the server hosting the instance.

When a user uploads media content (e.g., images) to our services, the files are typically saved to a designated directory on the server's filesystem. Our instances use a structure where media files are organized based on their content type and date of upload, making it easier to manage and retrieve them when needed.

For example, media files may be stored in directories like:

```bash
/media/
   └── attachments/
       ├── preview/
       ├── original/
       └── small/
```

In this structure, the "attachments" directory contains subdirectories for different sizes or versions of the uploaded media files, such as "preview" for thumbnail images, "original" for the original uploaded files, and "small" for smaller versions optimized for display.

It's important to note that the service's instances can be customized and configured by instance administrators, so the actual storage location and structure may vary based on their preferences and setup. Additionally, some instances may utilize external storage services or cloud storage providers (such as Amazon S3 or Google Cloud Storage) for media storage, especially for larger instances or to offload storage requirements from the server's local filesystem.
