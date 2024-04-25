# Core

It is the only centralized part of the application.

## Components

### Geo Service

It is golang gRPC server.

#### Endpoints

#### Entities

### Payments service

It is golang gRPC(❓) server.

#### Endpoints

#### Entities

### Plugin Store

It is golang gRPC server.

Possible plugins:
- personalized GPT assistent (voiced);
- writing textx assistent;

#### Endpoints

#### Entities

### Zookeepers Manager

It is golang gRPC server. It is dedicated for storing plugins and customers of it.
Besides, for some plugins it is okay to use resources of user's machine. So, it is reason why it is reasonable to build client apps:
- iOS modile app
- android mobile app
- windows desktop app
- linux desktop app
- macOS desktop app

#### Endpoints

#### Entities
