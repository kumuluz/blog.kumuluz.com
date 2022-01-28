---
layout: post
title:  "New releases of KumuluzEE OpenAPI MP and Health"
date:   2020-11-02
author: urbim
categories: [Product, Developers]
tags: [KumuluzEE OpenAPI, KumuluzEE Health, Microprofile, JavaEE]
---

We have just released new versions of [KumuluzEE OpenAPI MP](https://github.com/kumuluz/kumuluzee-openapi-mp) and [KumuluzEE Health](https://github.com/kumuluz/kumuluzee-health). New features include a Maven plugin which generates OpenAPI schema at compile-time, a new health check for Kafka clusters and integration between the two extensions.

<!--more-->

## [KumuluzEE OpenAPI MicroProfile 1.3.0](https://github.com/kumuluz/kumuluzee-openapi-mp/releases/tag/v1.3.0)

This version of _KumuluzEE OpenAPI MicroProfile_ brings a new Maven plugin which generates OpenAPI schema at compile-time and a new SPI interface which can be used to extend the generated schema.

To use the new Maven plugin add it to `pom.xml`:

```xml
<plugin>
    <artifactId>kumuluzee-openapi-mp-maven-plugin</artifactId>
    <groupId>com.kumuluz.ee.openapi</groupId>
    <version>${kumuluzee-openapi-mp.version}</version>
    <executions>
        <execution>
            <goals>
                <goal>generate</goal>
            </goals>
        </execution>
    </executions>
</plugin>
```

On next build the schema will be available in `target/generated/openapi.yaml` and `target/generated/openapi.json`. For more information about the maven plugin, see [README](https://github.com/kumuluz/kumuluzee-openapi-mp#openapi-maven-plugin).

The new SPI interface allows extension developers to extend the generated schema. To use it implement the `com.kumuluz.ee.openapi.mp.spi.OasFilterProvider` interface and register it with a service file.

## [KumuluzEE Health 2.3.0](https://github.com/kumuluz/kumuluzee-health/releases/tag/v2.3.0)

This release of _KumuluzEE Health_ brings a new health check for Kafka clusters, integration with KumuluzEE OpenAPI MP and a minor bugfix.

The new health check allows you to monitor the health status of your Kafka cluster. To use it add the `kafka-clients` dependency (already included in [`kumuluzee-streaming`](https://github.com/kumuluz/kumuluzee-streaming)) and activate it in the configuration framework. For example in `config.yml`:

```yaml
kumuluzee:
  health:
    checks:
      kafka-health-check:
        bootstrap-servers: localhost:9095,localhost:9096,localhost:9097
        minimum-available-nodes: 2
        request-timeout-ms: 1000
```

For more information see [README](https://github.com/kumuluz/kumuluzee-health#kafkahealthcheck).

We have integrated KumuluzEE Health with [KumuluzEE OpenAPI MP](https://github.com/kumuluz/kumuluzee-openapi-mp) extension. You can now add `/health`, `/health/ready` and `/health/live` endpoints to OpenAPI schema by activating the integration in the configuration framework. For example in `config.yml`:

```yaml
kumuluzee:
  health:
    openapi-mp:
      enabled: true
```

We are excited to bring these two new releases into your hands!
