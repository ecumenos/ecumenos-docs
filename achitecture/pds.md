# PDS (Personal Data Server)

PDS dedicated for storing profile data, direct/group messages, and posts & quick posts that are placed on personal page.

## Components

### Blockchain Peer

#### Description
The service dedicated for:
- storing of chains of actions with accounts (creation, deletation, transitions). It is sync with other PDSs;
- storing state of location all accounts (World State);

location of account looks like:
```json
{
    "aid": "1234567890",
    "pid": "2345678901",
    "oid": "3456789012"
}
```
Where `aid` = `account id`, `pid` = `PDS id`, `oid` = `orbis socialis id`.

### Accounts Ledger

#### Description
The service dedicated for:
- CRUD actions with account records;
- providing authentication functionality like (un)authorization;
- sending an account's data to next PDS services cluster while transition on an account to another PDS;
- providing generation & storing IDs functionality;

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
