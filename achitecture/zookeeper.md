# Zookeeper

This service act as DNS server.
It stores data about Orbis Socialis (plural) and their domain names.
Besides, it stores PDSs in the zookeeper network.

## Components

### Zookeeper

It is golang gRPC server.

#### Description

This service has next functionality:

- holders:
    - registration;
    - change password;
    - sign in;
    - refreshing token;
    - sign out;
- PDSs:
    - registration;
    - check status of instance registration;
    - monitoring;
- Orbises Socialis:
    - registration;
    - check status of instance registration;
    - monitoring;

#### Endpoints

- System:
    - endpoint for checking if the service is alive & getting service's information (`getInfo`)
- Holders:
    - endpoint for registration the holder account (`registerHolder`);
    - endpoint for confirmation of registration the holder account (`confirmHolderRegistration`);
    - endpoint for modifying of the holder account (`modifyHolder`);
    - endpoint for changing a password of the holder account (`changeHolderPassword`);
    - endpoint for retrieving holder account information (`getHolder`);
    - endpoint for deleting holder account information (`deleteHolder`);
    - auth:
        - endpoint for signing in (`signIn`);
        - endpoint for refreshing token (`refreshToken`);
        - endpoint for signing out (`signOut`);
- Zookeepers:
    - endpoint for retrieving list of Zookeepers (`getZookeepersList`);
    - endpoint for creation of record of new Zookeeper (`registerZookeeper`);
- PDSs:
    - endpoint for retrieving list of PDSs (`getPDSsList`);
    - endpoint for joining the waitlist for PDS registration (`joinWaitlistOfPDSRegistration`);
    - endpoint for registration of PDS instance (`registerPDS`);
- Orbises Socialis:
    - endpoint for retrieving list of Orbises Socialis (`getOrbisesSocialisList`);
    - endpoint for joining the waitlist for Orbis Socialis registration (`joinWaitlistOfOrbisSocialisRegistration`);
    - endpoint for registration of Orbis Socialis instance (`registerOrbisSocialis`);

#### Entities

##### Holder

| Field name                        | Type                                                               |
|-----------------------------------|--------------------------------------------------------------------|
| *id                               | numeric string                                                     |
| emails                            | array of email strings                                             |
| phone_numbers                     | array of phone number strings                                      |
| avatar_image_url                  | URL string                                                         |
| countries                         | array of country codes strings                                     |
| languages                         | array of language codes strings                                    |
| *created_at                       | datetime                                                           |
| last_modified_at                  | datetime                                                           |
| *password_hash                    | string                                                             |
| *confirmed                        | boolean                                                            |
| *confirmation_code                | string                                                             |

##### PDS

| Field name                        | Type                                                          |
|-----------------------------------|---------------------------------------------------------------|
| *id                               | numeric string                                                |
| *zookeeper_id                     | numeric string                                                |
| *name                             | string (max: 50)                                              |
| *location                         | Geography Data Type                                           |
| *capacity                         | numeric                                                       |
| *created_at                       | datetime                                                      |
| *alive                            | boolean                                                       |
| *is_open                          | boolean                                                       |
| *last_pinged_at                   | datetime                                                      |
| *seed                             | integer                                                       |
| *owner_id                         | numeric string                                                |
| *url                              | URL string                                                    |
| *register_additional_requirements | `enum RegistrationRequirements`                               |
| *forbidden_countries              | array of country codes strings                                |
| *forbidden_ips                    | array of strings (IP addresses (IPv4 & IPv6))                 |
| *api_key_hash                     | string (generated by nano and hashed)                         |

```ts
enum RegistrationRequirements {
    InviteCode
    None
}
```

##### Orbis Socialis

| Field name                        | Type                                                         |
|-----------------------------------|--------------------------------------------------------------|
| *id                               | numeric string                                               |
| *zookeeper_id                     | numeric string                                               |
| *name                             | string (max: 50)                                             |
| *location                         | Geography Data Type                                          |
| *domain_name                      | string                                                       |
| *capacity                         | numeric                                                      |
| *created_at                       | datetime                                                     |
| *alive                            | boolean                                                      |
| *is_open                          | boolean                                                      |
| *last_pinged_at                   | datetime                                                     |
| *owner_id                         | numeric string                                                |
| *url                              | URL string                                                   |
| *register_additional_requirements | `enum RegistrationRequirements`                              |
| *forbidden_countries              | array of country codes strings                               |
| *forbidden_ips                    | array of strings (IP addresses (IPv4 & IPv6))                |
| *api_key_hash                     | string (generated by nano and hashed)                        |

Domain name requirements:
- min length: 3;
- max length: 50;
- must contain: `.` and min 1 symbol before and after dot;

##### Zookeeper

| Field name               | Type                                                               |
|--------------------------|--------------------------------------------------------------------|
| *id                      | numeric string                                                     |
| *name                    | string (max: 50)                                                   |
| *address_suffix          | string (min: 1, max: 10)                                           |
| *pds_capacity            | numeric                                                            |
| *orbis_socialis_capacity | numeric                                                            |
| *created_at              | datetime                                                           |
| *alive                   | boolean                                                            |
| *last_pinged_at          | datetime                                                           |
| *owner_id                | numeric string                                                     |
| *url                     | URL string                                                         |

#### Technology stack:

Programming language: golang

Transport: gRPC

Databases: PostgreSQL

### Admin

SSR frontend application with REST API endpoints.
NextJS is good technology for this service.

#### Description

The service provides functionality for configuring the PDS.

#### Technology stack:

Programming language: golang

Transport: REST API+SSR

Databases:

## Decisions
