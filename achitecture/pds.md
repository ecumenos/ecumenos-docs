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

- search:
    - endpoint for searching of Orbis Socialis contant (use Orbis Socialis search);
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

### Blockchain Peer

The service is golang gRPC server that serves as blockchain peer.

#### Description
The service dedicated for:
- storing of chains of actions with accounts (creation, deletation, transitions). It is sync with other PDSs;
- storing state of location all accounts (World State);

location of account looks like:



PoA (Proof of Authority) looks most preferable for now.

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

### Accounts Ledger

It is golang gRPC server that oprates with account's profile data and account's personal posts, quick-posts, and albums.

#### Description

The service dedicated for:
- CRUD actions with account records;
- providing authentication functionality like (un)authorization;
- sending an account's data to next PDS services cluster while transition on an account to another PDS;
- providing generation & storing IDs functionality;

### Admin

SSR frontend application with REST API endpoints.
NextJS is good technology for this service.

#### Description

The service provides functionality for configuring the PDS.

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
Keep in mind that an accounts are portable and the account that was created in the PDS could be transfered to some another PDS.
