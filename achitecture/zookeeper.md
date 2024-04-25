# Zookeeper

This service act as DNS server.
It stores data about Orbis Socialis (plural) and their domain names.
Besides, it stores PDSs in the zookeeper network.

## Components

### Zookeeper

It is golang gRPC server.

#### Description

#### Endpoints

#### Entities

##### PDS

| Field name        | Type                                                               |
|-------------------|--------------------------------------------------------------------|
| *id               | numeric string                                                     |
| *zookeeper_id     | numeric string                                                     |
| *name             | string (max: 50)                                                   |
| *location         | Geography Data Type                                                |
| *capacity         | numeric                                                            |
| *created_at       | timedate (RFC3339, example "2006-01-02T15:04:05Z07:00")            |
| *alive            | boolean                                                            |
| *last_pinged_at   | timedate (RFC3339, example "2006-01-02T15:04:05Z07:00")            |
| *seed             | integer                                                            |
| *owner_email      | email string                                                       |
| *password_hash    | string                                                             |
| *url              | URL string                                                         |

##### Orbis Socialis

| Field name        | Type                                                               |
|-------------------|--------------------------------------------------------------------|
| *id               | numeric string                                                     |
| *zookeeper_id     | numeric string                                                     |
| *name             | string (max: 50)                                                   |
| *domain_name      | string                                                             |
| *capacity         | numeric                                                            |
| *created_at       | timedate (RFC3339, example "2006-01-02T15:04:05Z07:00")            |
| *alive            | boolean                                                            |
| *last_pinged_at   | timedate (RFC3339, example "2006-01-02T15:04:05Z07:00")            |
| *owner_email      | email string                                                       |
| *password_hash    | string                                                             |
| *url              | URL string                                                         |

Domain name requirements:
- min length: 3;
- max length: 50;
- must contain: `.` and min 1 symbol before and after dot;

##### Zookeeper

| Field name               | Type                                                               |
|--------------------------|--------------------------------------------------------------------|
| *id                      | numeric string                                                     |
| *name                    | string (max: 50)                                                   |
| *prefix                  | string (min: 1, max: 10)                                           |
| *pds_capacity            | numeric                                                            |
| *orbis_socialis_capacity | numeric                                                            |
| *created_at              | timedate (RFC3339, example "2006-01-02T15:04:05Z07:00")            |
| *alive                   | boolean                                                            |
| *last_pinged_at          | timedate (RFC3339, example "2006-01-02T15:04:05Z07:00")            |
| *owner_email             | email string                                                       |
| *password_hash           | string                                                             |
| *url                     | URL string                                                         |

### Admin

SSR frontend application with REST API endpoints.
NextJS is good technology for this service.

#### Description

The service provides functionality for configuring the PDS.

## Decisions
