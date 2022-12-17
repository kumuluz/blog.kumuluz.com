---
layout: post
title:  "KumuluzEE Health 2.4.4 released"
date:   2022-11-30
author: urbim
categories: [Product, Announcement, Developers]
tags: [KumuluzEE, Java EE, Microservices]
---

We have released a minor release of KumuluzEE Health 2.4.4 with the following:
This patch release fixes a initialization bug, where built-in health checks were not initialized from configuration.
Bugs:
- Fixed built-in health check configuration detection - use getMapKeys and getListSize instead of yaml-specific Map/List detection, that was removed in KumuluzEE 4.1.0

__Note: This release of KumuluzEE Config MP requires the KumuluzEE 4.1.0 or higher in order to work correctly.
Consequently, Java 11 or higher is also required.__


Check out the release on GitHub: [KumuluzEE Health v2.4.4]( https://github.com/kumuluz/kumuluzee-health/releases/tag/v2.4.4)
