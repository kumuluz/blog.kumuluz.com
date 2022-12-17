---
layout: post
title:  "KumuluzEE JCache 2.0.0 released"
date:   2022-12-03
author: urbim
categories: [Product, Announcement, Developers]
tags: [KumuluzEE, Java EE, Microservices]
---

We are excited to announce the next major version of KumuluzEE JCache - 2.0.0. This release adds support for the newest KumuluzEE version 4 and adds support for Java 17 LTS and Java 18.

This release also uses the new configuration prefix `kumuluzee.jcache.caffeine.caches` instead of `kumuluzee.jcache.caffeine.caffeine.jcache` and adds support for the entire configuration framework instead only yaml files, including overriding properties from ENV variables.

##### An example of migration to the new configuration prefix:

Old:

<pre>
kumuluzee:
  jcache:
    caffeine:
      <b>caffeine.jcache:</b>
        default:
          policy:
            maximum:
              size: 10000
        exampleCache:
          policy:
            eager-expiration:
              after-write: "1s"
</pre>

New:

<pre>
kumuluzee:
  jcache:
    caffeine:
      <b>caches:</b>
        default:
          policy:
            maximum:
              size: 10000
        exampleCache:
          policy:
            eager-expiration:
              after-write: "1s"
</pre>

Since the support for Java 1.8 is dropped by KumuluzEE 4.0.0, the KumuluzEE JCache 2.0.0 also drops support for Java 1.8. 

#### Features

- Added support for KumuluzEE 4.0.0 and above
- Added support for Java 17 LTS and Java 18

#### Bugs

- Fixed initialization from configuration - do not rely on a bug in core, instead use getMapKeys/getListSize
- Fixed initialization from configuration - use the whole configuration framework instead of only yaml files



__Note: This release of KumuluzEE Config MP requires the KumuluzEE 4.0 or higher in order to work correctly.
Consequently, Java 11 or higher is also required.__


Check out the release on GitHub: [KumuluzEE JCache v2.0.0](https://github.com/kumuluz/kumuluzee-jcache/releases/tag/v2.0.0)

