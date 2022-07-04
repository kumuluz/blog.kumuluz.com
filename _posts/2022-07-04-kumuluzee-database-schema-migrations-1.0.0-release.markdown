---
layout: post
title:  "Announcing KumuluzEE Database Schema Migrations 1.0.0 release"
date:   2022-07-04
author: dinm
categories: [Product, Announcement, Developers]
tags: [KumuluzEE, Microservices, Migrations, KumuluzEE Database Schema Migrations, Liquibase]
---

We are pleased to announce the first stable release of the KumuluzEE Database Schema Migration extension for the KumuluzEE microservice framework.

The extension provides an easy way to migrate database schemas with Liquibase.
It allows migrations at application startup or, if necessary, when the application is already running.
Therefore, the extension can speed up the development process by ensuring that database schemas are up to date when the application starts.

The extension can be configured in the common KumuluzEE configuration file.
The only requirement is a configured data source where the schema migrations can be performed.
Since the extension is based on the Liquibase, all data sources supported by the Liquibase can be used in conjunction with this extension.

The main advantages of the extension are:
  - Ensures that the database schema is up to date
  - Eliminates the need to perform migrations manually
  - Allows database schema migrations to be managed in the runtime
  - Enables database schema migrations for multiple databases
  - Manages database schema migrations on a per-application basis
  - Optionally starts each application run with fresh database state
  
To get started quickly, configure the desired data source and link the migration to it.
```yaml
kumuluzee:
  datasources:
    - jndi-name: jdbc/ExampleDS
      connection-url: jdbc:postgresql://localhost:5432/postgres
      username: postgres
      password: postgres
      pool:
        max-size: 20
  database-schema-migrations:
    liquibase:
      changelogs:
        - jndi-name: jdbc/ExampleDS
          startup:
            drop-all: false
            update: true
```

For step-by-step guide (example) see [KumuluzEE migrations with Liquibase](https://github.com/kumuluz/kumuluzee-samples/tree/master/kumuluzee-database-schema-migrations-liquibase).
