---
layout: post
title: "Deprecation Notice for Web Questionnaires"
date: 2026-10-12 08:00:00 +0100
categories: announcement
author: Selina
---

We hereby want to officially announce the deprecation of the web version of ESMira. This option as received little use by us and, to our knowledge, by others. Due to inherent limitations, we were not able to support this feature, leaving it in an incomplete state. For this reason, we have decided to remove it in an upcoming release. If you use web questionnaires, we ask you to keep an eye out for update announcements, as we will there note there separately once we do remove this component.

Web questionnaires made sense at the time they were developed, when ESMira still had no iOS version, and the pool of available items was limited to simple options like Likert and visual analog scales. Over time, ESMira not only received an iOS version, but also features like the message and reward systems that require one persistent user, and item types like battery level, location, and compass, that make direct use of the device's sensors. Not to mention basic features like notifications. None of these features can be used in the web version.

Overall, web questionnaires offer very little of what ESMira aims to provide, while increasing our technical debt. David Lewetz has worked on removing the web version, in order to keep things focused. The questionnaire preview feature previously has relied on the web questionnaire, which is why it was also out of date. David has also reworked that feature, meaning it should now work better with newer item types that were unsupported by the web questionnaire.
