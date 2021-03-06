---
layout: post
title:  "KumuluzEE OpenAPI in action"
date:   2017-10-27
author: zvoneg
categories: [Product, Developers]
tags: [KumuluzEE OpenAPI, Swagger-UI]
---

**KumuluzEE OpenAPI was recently updated!** with separate dependency for the OpenAPI UI. Check [KumuluzEE OpenAPI - Updated](https://blog.kumuluz.com/product/developers/2018/01/14/kumuluzee-openapi-usage-updated)

KumuluzEE OpenAPI extension allows you to document microservice APIs using OpenAPI v3 compliant annotations. Extension will automatically hook-up servlet that will 
serve your API specifications on endpoint ```/api-specs/<jax-rs application-base-path>/openapi.[json|yaml]```. Furthermore, extensions allows you to integrate Swagger-UI into your
microservice that will visualize APIs documentation and allow you to interact with your APIs resources.
 
More details: [OpenAPI v3 Specification](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.0.md).

## Usage

You can enable KumuluzEE OpenAPI support by adding the following dependency:
```xml
<dependency>
    <groupId>com.kumuluz.ee.openapi</groupId>
    <artifactId>kumuluzee-openapi</artifactId>
    <version>${kumuluzee-openapi.version}</version>
</dependency>
```

## OpenAPI configuration

When kumuluzee-openapi dependency is included in the project, you can start documenting your REST API using [Swagger-Core Annotations](https://github.com/swagger-api/swagger-core/wiki/Annotations-2.X).

### Documenting application class
```java
@SecurityScheme(name = "openid-connect", type = SecuritySchemeType.OPENIDCONNECT, 
                openIdConnectUrl = "http://auth-server-url/.well-known/openid-configuration")
@OpenAPIDefinition(info = @Info(title = "Rest API", version = "v1", description = "JavaSI API for managing conference.", 
                    security = @SecurityRequirement(name = "openid-connect"), servers = @Server(url ="http://localhost:8080/v1")))
@ApplicationPath("v1")
public class JavaSiApplication extends Application {...}
```

### Documenting resource class and operations
```java
@Path("sessions")
@Consumes(MediaType.APPLICATION_JSON)
@Produces(MediaType.APPLICATION_JSON)
public class SessionsResource {

    @Operation(description = "Returns list of sessions.", summary = "Sessions list", tags = "sessions", responses = {
            @ApiResponse(responseCode = "200",
                    description = "List of sessions",
                    content = @Content(
                            schema = @Schema(implementation
                            = Session.class)),
                    headers = {@Header(name = "X-Total-Count",
                            schema = @Schema(type = "int"))}
                    )})
    @SecurityRequirement(name = "openid-connect")
    @GET
    public Response getSessions() {...} 
    ...
}
```

<!--more-->

## Accessing API specification

Build and run project using:

```bash
mvn clean package
java -jar target/${project.build.finalName}.jar
```

After startup API specification will be available at:

**http://<-hostname-:<-port->/api-specs/<-application-base-path->/openapi.[json,yaml]**

Example:

http://localhost:8080/api-specs/v1/openapi.json



Read more about extension at [KumuluzEE OpenAPI](https://github.com/kumuluz/kumuluzee-openapi/blob/master/README.md) and explore sample project at [KumuluzEE OpenAPI Sample](https://github.com/kumuluz/kumuluzee-samples/tree/master/kumuluzee-openapi).
