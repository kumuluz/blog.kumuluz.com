---
layout: post
title:  "KumuluzEE GraphQL 1.1.0 released!"
date:   2021-02-09
author: urbim
categories: [Product, Announcement, Developers]
tags: [KumuluzEE, Java EE, Microservices, GraphQL]
---

We are excited to announce a new minor release - KumuluzEE GraphQL 1.1.0. This release includes a new MicroProfile
compatible implementation, we have updated the Graph*i*QL (GraphQL UI) to support better schema exploration and fixed
some bugs in our existing implementation.

To use the new MP-compatible implementation use the following dependency:

```xml
<dependency>
    <groupId>com.kumuluz.ee.graphql</groupId>
    <artifactId>kumuluzee-graphql-mp</artifactId>
    <version>${graphql.version}</version>
</dependency>
```

Note that the existing implementation (artifact `kumuluzee-graphql`) is still being updated. However, we advise new
users to start with the MP implementation since this implementation is more likely to receive new features in the future.

Graph*i*QL now includes the [explorer plugin](https://github.com/OneGraph/graphiql-explorer),
which enables you to interactively construct a query or mutation. This makes schema exploration and API usage
even easier.

Integration with KumuluzEE REST has also been revamped to be more intuitive and future-proof.
Sort and filter arguments are now string-based and limit/offset are now top level arguments.
This makes queries more readable and easier to process. The `QueryParameters` object can be constructed and used
with any KumuluzEE REST implementation (currently `StreamUtils` and `JPAUtils`).

The samples for MP-compatible implementation are already available:

- [kumuluzee-graphql-jpa-simple](https://github.com/kumuluz/kumuluzee-samples/tree/master/kumuluzee-graphql-jpa-simple)
- [kumuluzee-graphql-jpa-security](https://github.com/kumuluz/kumuluzee-samples/tree/master/kumuluzee-graphql-jpa-security)
- [kumuluzee-graphql-advanced](https://github.com/kumuluz/kumuluzee-samples/tree/master/kumuluzee-graphql-advanced)


#### Features:

- Added MP-compatible implementation by SmallRye
- Added Graph*i*QL Explorer plugin

#### Enhancements:

- Converted GraphQL manual kumuluzee-rest processing to StreamUtils
- Upped dependency versions

#### Bugs:

- Fixed Graph*i*QL servlet mapping
- Fixed pagination limit bug

Check out the release on GitHub: [KumuluzEE GraphQL v1.1.0](https://github.com/kumuluz/kumuluzee-graphql/releases/tag/v1.1.0)
