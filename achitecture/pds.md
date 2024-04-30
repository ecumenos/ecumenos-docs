# PDS (Personal Data Server)

PDS dedicated for storing profile data, direct/group messages, and posts & quick-posts that are placed on personal page.

## Components

### BFF (Backend for Frontend)

It is golang REST API server that exposes endpoint for web and mobile frontend applications.

#### Description

It serves as gateway (REST API).
This service works like proxy for WRITE commands and it can interact with database directly for READ queries.
The service interacting with Orbis Socialis (pl.).

#### Endpoints

- endpoint for validation of PDS & Orbis Socialis invite codes(`POST /invite-code/validation` use body for distinguishing PDS & Orbis Socialis);
- search:
    - endpoint for searching of Orbis Socialis content (use Orbis Socialis search);
    - endpoint for searching accounts;
- feed:
    - endpoints for getting feed;
- authorization:
    - endpoint for creating an account;
    - endpoint for retrieving an account's data;
    - endpoint for updating an account's data;
    - endpoint for deleting an account;
    - endpoint for creating a session;
    - endpoint for refreshing a session;
    - endpoint for closing a session;
    - endpoint for updating password'
- posts:
- quick-posts:
- groups:

#### Technology stack:

Programming language: golang

Transport: REST API

Databases: Redis,

### Blockchain Peer

The service is golang gRPC server that serves as blockchain peer.

#### Description
The service dedicated for:
- storing of chains of actions with accounts (creation, deletation, transitions). It is sync with other PDSs;
- storing state of location all accounts (World State);
Good choice for storage is local instance of SQLite.
Use `MD6-256` as hash function.

When the service is starting up it calls zookeeper to get full list of PDSs.
After the service call validator PDS from the list to get last transactions from shutting down timepoint.
Then transactions are applied and World State is updated.
After the service can process requests.

Validator is chosen by zookeeper. Beside, zookeeper should check status of all PDSs to choose validator by the best way for next time.
When the service call some other service and it doesn't response for 30s it should call zookeeper to report it. Then zookeeper do the request by itself and if it doesn't response it write this information to the register and this information will be considered next time when validator is choosing.

#### How the Blockchain works

It is a blockchain network for storing account's references.
The network should be synchronized inside of itself.
All peers should store full history of transactions.
Besides, it should also store "state of world". It is current state of data inside of the distributed ledger.

Structure of state of world entities:

```json
{
    "aid": "1234567890",
    "pid": "2345678901",
    "oid": "3456789012"
}
```

Where `aid` = `account id`, `pid` = `PDS id`, `oid` = `orbis socialis id`.

Transactions are operations with that objects.
Structure of a transaction should looks like:
```json
{
    "op": "create" | "modify" | "delete",
    "field": "aid" | "pid" | "oid",
    "value": "...." | null "{{aid}}::{{pid}}::{{oid}}",
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
        "value": "1234567890::2345678901::3456789012",
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
- endpoint for getting state of accounts (`GET/accounts?ids=1234567890,1234567891,1234567892`) it should works only with IDs

#### Entities

#### Technology stack:

Programming language: golang

Transport: gRPC

Databases: SQLite

### Accounts Service

It is golang gRPC server that operates with account's profile data and account's personal posts, quick-posts, and albums.

#### Description

The service dedicated for:
- account & account's data functionality
- providing uniqueness of ID generation
- messenger functionality
- authorization & authentication functionality
- interaction with other PDS clusters
- mailer functionality

#### Technology stack:

Programming language: golang

Transport: gRPC

Databases: ArangoDB

#### Endpoints:

#### Entities

##### Account Entity

| Field name                        | Type                                                               |
|-----------------------------------|--------------------------------------------------------------------|
| *id                               | numeric string                                                     |
| *handle_name                      | string                                                             |
| *address                          | string                                                             |
| *full_name                        | string (max: 50)                                                   |
| emails                            | array of email strings                                             |
| phone_numbers                     | array of phone number strings                                      |
| avatar_image_url                  | URL string                                                         |
| header_image_url                  | URL string                                                         |
| bio                               | string (max: 1024)                                                 |
| countries                         | array of lowercased strings (ISO 3166-1 alpha-3 country code)      |
| languages                         | array of lowercased strings (ISO 639-2:1998 alpha-3 language code) |
| *created_at                       | datetime                                                           |
| last_modified_at                  | datetime                                                           |
| last_seen_at                      | datetime                                                           |
| *password_hash                    | string                                                             |
| *public_key                       | string                                                             |
| *private_key                      | encrypted string                                                   |
| birthday                          | datetime                                                           |
| sex                               | `enum Sex`                                                         |
| *account_id                       | numeric string                                                     |
| *perm_read_profile_info           | enum `Permission`                                                  |
| *perm_read_profile_posts          | enum `Permission`                                                  |
| *perm_comment_profile_posts       | enum `Permission`                                                  |
| *perm_react_profile_posts         | enum `Permission`                                                  |
| *perm_read_profile_qposts         | enum `Permission`                                                  |
| *perm_comment_profile_qposts      | enum `Permission`                                                  |
| *perm_react_profile_qposts        | enum `Permission`                                                  |
| *notification_direct_messages     | boolean                                                            |
| *notification_group_messages      | boolean                                                            |
| *notification_followed_content    | boolean                                                            |
| *notification_group_actions       | boolean                                                            |
| *notification_group_content       | boolean                                                            |
| *notification_group_topics        | boolean                                                            |
| *notification_group_topic_records | boolean                                                            |
| *theme_color_mode                 | enum `ColorMode`                                                   |
| *theme_zoom                       | integer (from 50% to 200%)                                         |
| *theme_msg_format                 | enum `MessageFormat`                                               |
| *theme_name_format                | enum `NameFormat`                                                  |
| *time_format                      | 12/24                                                              |

```ts
enum Sex {
    Male
    Female
}
```

```ts
enum Permission {
    Public
    Private
    OnlyMe
}
```

```ts
enum ColorMode {
    Dark
    Light
}
```

```ts
enum MessageFormat {
    SenderMessageDatetime
    SenderDatetimeMessage
}
```

```ts
enum NameFormat {
    FullAndHandle
    JustHandle
}
```

Handle name requirements:
- min length: 3;
- max length: 50;
- allowed chars:
    - `A-Z`;
    - `a-z`;
    - `Α-Ω`;
    - `α-ω`;
    - `1-9`;
    - `Ē`, `ē`, `Ā`, `ā`, `Ō`, `ō`, `Ī`, `ī`, `Ū`, `ū`, `Č`, `č`, `Ď`, `ď`, `É`, `é`, `Ě`, `ě`, `Í`, `í`, `Ř`, `ř`, `Š`, `š`, `Á`, `á`, `Ą`, `ą`, `Ć`, `ć`, `Ę`, `ę`, `Ł`, `ł`, `Ň`, `ň`, `Ń`, `ń`, `Ó`, `ó`, `Ś`, `ś`, `Ť`, `ť`, `Ú`, `ú`, `Ů`, `ů`, `Ý`, `ý`, `Ž`, `ž`, `Ź`, `ź`, `Ż`, `ż`, `ẞ`, `ß`, `Ä`, `ä`, `Ö`, `ö`, `Ü`, `ü`, `Æ`, `æ`, `Ø`, `ø`, `Å`, `å`;
    - special chars: `_`, `-`, `+`, `$`, `€`, `£`, `¥`, `₣`, `₹`, `₪`, `₩`, `₴`;

Address composition: `@{{handle_name}}#{{domain_name}}::{{zookeeper_suffix}}`

Example:

zookeeper_suffix=zk_ukr1,
handle_name=john_doe
domain_name=lviv.ukr1

account address=@john_doe#lviv.ukr1::zk_ukr1
orbis_socialis=#lviv.ukr1::zk_ukr1
zookeeper=::zk_ukr1

##### Sessions

jwt.io

| Field name                   | Type                                                    |
|------------------------------|---------------------------------------------------------|
| *id                          | numeric string                                          |
| *provider_pds_id             | numeric string                                          |
| *account_id                  | numeric string                                          |
| *token                       | string                                                  |
| *refresh_token               | string                                                  |
| *expired_at                  | datetime                                                |
| *created_at                  | datetime                                                |

### Admin

SSR frontend application with REST API endpoints.
NextJS is good technology for this service.

#### Description

The service provides functionality for configuring the PDS.

#### Technology stack:

Programming language: golang

Transport: REST API+SSR

Databases: PostgreSQL

## Decisions

### ID generation

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

### Cryptography Security

Encryption is done by some asymmetric algorithm.
Public key is stored at account profile.
Private key is encrypted by symmetric encryption with account's password and stored in account profile.
