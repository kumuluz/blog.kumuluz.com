---
layout: post
title:  "KumuluzEE Database Schema Migrations - Liquibase extension"
date:   2022-02-26
author: dinm
categories: [Product, Developers]
tags: [KumuluzEE Database Schema Migrations, Liquibase]
---

In the rapidly growing world of automation, there is a constant need for application updates.
Every change made to the application is nowadays version controlled, making it easy to automate deployment and, if necessary, roll back changes.
Today, it is not uncommon to have multiple versions of an application deployed on the same day.
Following this pattern, it quickly becomes clear that database schemas need to be managed in the same way.

KumuluzEE is pleased to announce the Liquibase extension for database schema migration.
It allows you to migrate your schemas right at the application startup, so that you get the desired database state every time you run the application.
Moreover, it also offers a possibility to drop the database before migration, making it a perfect choice for development and testing purposes.
Not to be confused, Liquibase migrations via the Maven plugin are still infallible, especially in environments where we want to have full control.

To get started with the Liquibase extension, 
all you need to do is add the Liquibase database schema migration extension to your existing pom file.
```xml
<dependency>
    <groupId>com.kumuluz.ee.database-schema-migrations</groupId>
    <artifactId>kumuluzee-database-schema-migrations-liquibase</artifactId>
    <version>${kumuluzee-database-schema-migrations.version}</version>
</dependency>
```

Furthermore, the known KumuluzEE configuration file has to be adjusted.
```yaml
kumuluzee:
  ...
  database-schema-migrations:
    liquibase:
      changelogs:
        - jndi-name: jdbc/example-db
          file: db/changelog-master.xml
          startup:
            drop-all: false           # default: false  
            update: true              # default: false
```

The above configuration instructs the Liquibase extension to update the current database schemas.
The update is performed when the application is started.
This involves making changes to a pre-configured data source with the appropriate JNDI name, which in our case is `jdbc/example-db`.
What changes will take place is defined in a Liquibase changelog file (`db/changelog-master.xml`).

After we have everything set up, we can launch our application and see how it manages the migrations for us.

For more information and detailed walkthrough, we recommend you take a look at the
[KumuluzEE database schema migrations](https://github.com/kumuluz/kumuluzee-database-schema-migrations#kumuluzee-database-schema-migrations) documentation on GitHub.

If you are not yet familiar with [Liquibase](https://liquibase.org/), we also recommend you to give it a try.