---
layout: post
title: "Update on Upcoming Changes to Scheduling"
date: 2026-05-27 12:00:00 +0100
categories: update
author: Selina
---

Previously we have made an [announcement about upcoming changes to scheduling](https://kl-psychological-methodology.github.io/ESMira/announcement/2026/03/30/announcement-scheduling-changes.html).

The release of the new smartphone application version is coming closer, as we are internally testing the changes. And while we initially thought that the new system would necessitaty breaking changes, we rethought the problem and managed to find a backwards compatible solution. However, there are some caveats, so if you have an ongoing study and need to preserve the old scheduling system for consistency, please read on to find out what you have to do for this to work properly.

## New Study Setting 'Legacy Scheduling'

The old scheduling system has been preserved as a new setting for studies. Under _Study Settings_ > _Use Legacy Scheduling_ you can set a study to use the previous, 24-hour-interval based system. This setting is **off by default**, however, the update script to server version 3.6.0 will **turn it on for all existing studies**.

### Is it Necessary to Update?

Unless you spicifically need certain bugfixes, we would usually recommend against updating during an ongoing study. However, if you have an ongoing study and want to preserve the previous behavior for consistency, you might want to update your server. Once smartphones receive the update, they will activate legacy scheduling for all ongoing studies. If nothing changes, everything will go on as normal. Still, if you do not update the server, this new setting will not be part of the study file. That means if you change the study and a participant's phone downloads an update, or if a new participant joins the study, their phone interprets the missing legacy scheduling setting as a default value, and will use the new system. If you update the server the downloaded study file will include this setting, and studies should go on as normal.

On the other hand, if you haven't started with data collection yet, but have created your study already, our recommendation is to deactivate legacy scheduling, as the new system is more intuitive and should be overall more consistent.
