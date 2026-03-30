---
layout: post
title: "Announcement: Upcoming Breaking Changes to Scheduling"
date: 2026-03-30 12:00:00 +0100
categories: announcement
author: Selina
---

We hereby want to inform you about upcoming changes to the timing of specific settings in the scheduling of triggers, i.e., the notification system. I suspect that for most users this change will bring ESMira more in alignment with how they are expecting it to behave anyway. However, some of you might have come to expect the scheduling to behave a certain way, and therefore we want to announce these changes beforehand. The timeline on these is not certain yet, but most likely the change will happen sometime within the next two months.

## The Upcoming Change: What ESMira understands as a 'Day'

In _Filter and Trigger_, the scheduling section of studies, there are a few settings referencing 'days'. Specifically the filters '_Activation after_' and '_Expiration after_', which should ensure that a questionnaire is only available on certain days of the study, and the setting _Wait 1 days until first execution_ within repeating schedules.

What is counterintuitive about these settings is that 'days' here refers to 'Intervals of 24 hours since joining the study'. I.e., the time of day a study has been joined is relevant. For example, if a Questionnaire has the filter '_Expiration after 2 days_', and a participant joins at 11:00 AM, they can fill out the questonnaire at 10:00 AM on the second day, but won't be able to do so at 1:00 PM on that day.

Since not all participants will join at the same time of day, this behavior can make scheduling somewhat unpredictable. The issue gets compounded by the fact that we recently fixed a behavior where notifications on iOS would lead to a questionnaire, regardless of whether or not it was active. As the way the iOS version of the app schedules ahead notifications (and the app not being able to check if a questionnair is active at the time the notification happens), certain study configurations can now lead to participants in using iOS to receive notifications on their last study day, only to click on them and be greeted by a dialog telling them that the questionnaire is not active (which is another recent addition).

Therefore, we have decided to change the way ESMira interprets thes settings, away from a strict '24 hour intervals after the join timestamp' to a date based approach. This means ESMira will compare dates, which should also make it easier to think in study days with these options.

Going forward after the change, the '_Activation after_' and '_Expiration after_' filters will count the day a study is joined will count as _day 0_, ensuring that you indeed get _full study days_. The '_Wait 1 days until first execution_' option in schedules will wait till the next midnight, i.e., will wait _until day 1_ of the study. If two participants join on the same day, with one joining in the morning and the other in the evening of that day, they will both have the same scheduling the day after.

## What you have to do

Most likely you won't have do do anything. I suspect that this behavior is counterintuitive enough that most of you will see it as a bug anyway, and all you have to do is to wait for it to be fixed.

If you are currently planning a study that is sensitive for its timing, just be aware of this change, and try to think through how this might affect your schedules.

We have assumed that the current behavior will be unlikely to be what researchers want, which is why we have decided to change the behavior of the existing options, rather than preserve backwards compatibility and add new options (which would have to be similar in naming to the existing ones, and hence likely cause more confusion). However, **if you understand, use, and explicitly want the existing 24-Hour-Interval behavior, please make this known!**. We don't want to take away options that are wanted by users and actively in use, so please contact us, preferably in the [discussion forum on the ESMira GitHub repository](https://github.com/KL-Psychological-Methodology/ESMira/discussions).
