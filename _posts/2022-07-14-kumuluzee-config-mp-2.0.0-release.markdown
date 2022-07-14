---
layout: post
title:  "KumuluzEE MicroProfile Config 2.0.0 released"
date:   2022-07-14
author: urbim
categories: [Product, Announcement, Developers]
tags: [KumuluzEE, Java EE, Microservices]
---

We are excited to announce the next major release of KumuluzEE Config MP. KumuluzeEE Config MP 2.0.0 implements the
MicroProfile Config 2.0 specification, which includes many improvements, among others the support for the
`@ConfigProperties` annotation which extracts bulk config properties into a POJO, the API which allows developers to
determine the winning source for a configuration value, and more.

__Note: This release of KumuluzEE Config MP requires the KumuluzEE 4.1.0 or higher in order to work correctly.
Consequently, Java 11 or higher is also required.__

Some of the bigger changes in the MicroProfile Config 2.0 specification like property expressions
(configuration value interpolation) and configuration profiles were added to the core KumuluzEE and can be used with
or without KumuluzEE Config MP extension. To read more about these changes see the
[KumuluzEE 4.1.0 release notes](https://github.com/kumuluz/kumuluzee/releases/tag/v4.1.0).

The `@ConfigProperties` annotation allows bulk extraction of config properties into a CDI bean and works similarly to
the KumuluzEE native `@ConfigBundle` annotation. It works in the MicroProfile Config's environment and supports its
features (e.g. converters, custom `ConfigSource` implementations, ...). For example, take a look at the following class:

<!--more-->

```java
@ConfigProperties(prefix = "integrations.customer-service")
public class CustomerServiceConfig {
    @ConfigProperty(name = "host", defaultValue = "example.com")
    private String hostname;
    private int port = 8080; // 8080 is the default value
    private Optional<String> authorization;

    // getters
}
```

The `Config` API has also received some improvements. It includes a method to acquire a `ConfigValue` instance,
exposing metadata about the configuration value such as the configuration source that provided the value, its ordinal
and the raw value before property expression evaluation. Additionally, the converter mechanism has been exposed,
allowing manual conversion of arbitrary values through the `Config` API.

For all changes included in this release, see the
[MicroProfile Config 2.0 specification](https://github.com/eclipse/microprofile-config/releases/tag/2.0).

#### Features:

- Implemented MicroProfile Config 2.0 specification
- Migrated to KumuluzEE 4.x.x and dropped support for Java 1.8

#### Bugs:

- Fixed default value not being used when injecting `Optional` with the default value supplied by `@ConfigProperty` annotation

Check out the release on GitHub: [KumuluzEE Config MicroProfile v2.0.0](https://github.com/kumuluz/kumuluzee-config-mp/releases/tag/v2.0.0)
