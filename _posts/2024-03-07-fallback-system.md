---
layout: post
title: "Fallback System"
date: 2025-03-10 9:00:00 +0200
categories: feature
author: Selina
---

We are introducing a new feature to ESMira: the Fallback System. This feature, which will soon be available, will help make ESMira somewhat more robust.

## What does the Fallback System do?

The Fallback System allows you to connect two ESMira servers, allowing one server to store study configuration files on another server. This allows the other server to provide the instructions on how to join the study, as well as the study file for joining the study. The idea is to make the study available on a second server, so that potential participants can join the study even if the original server is temporarily unavailable.

To go a bit more into detail, the system works like this: Suppose there are two ESMira servers, let us call them _A_ and _B_. They are configured so that the server _A_ can use the server _B_ as fallback. When a user on server _A_ saves their study, a copy is sent to server _B_. Server _B_ saves this in a special location, so the studies on the servers do not mix (i.e., users on server _B_ do not suddenly gain access to studies on server _A_).

When a user on server _A_ publishes their study, they will find the study links amended by an additional 'fallback' URL parameter. This parameter encodes the web address of the fallback server, and is also present in the QR code. The publish page will also provide a link to the app install instruction page on the server _B_ (which should be identical to the page on server _A_).

Suppose that server _A_ now experiences some technical problem and goes offline for a while. Normally, the study would be inaccessible. However, the app install instruction on server _B_ still works. And what's more, the ESMira app is now clever enough to interpret the fallback parameter in the QR code. So when the user tries to join the study in the app, and server _A_ does not respond, it will automatically try to retrieve the study from server _B_. If it can, then the participant's app can join the study. The app will happily run the study and collect data, even while server _A_ remains offline. Once it is back up again, it will send all the data to it. This includes the initial "join" event, so you will still know when a participant has joined.

## In what situations is the Fallback System helpful?

ESMira in general is relatively robust in terms of connectivity. There are only a few functions that require a connection to the server, such as checking a reward code, or retrieving statistics for all participants for displaying graphs. However, the core functionality of collecting data and sending notifications fully work online. Most study participants should not even notice a server going offline for a while. Prospective participants seeking to join the study will of course need a connection to the server. This is unfortunate, because this is a somewhat critical moment, and some participants might not try again if joining the study does not work right away. The Fallback System tries to mitigate this case in particular, as each participant is valuable.

## Where the Fallback System cannot help

The system has some limitations. While QR codes and the new links to the study information and the app installation instructions will keep working as normal, when opened in the browser they cannot redirect by themself if the server is not reachable. This is the reason for the extra fallback app installation instructions link. If you want to be sure, you need to provide participants with both links. If you want to use just the QR code, then this will work for joining the study in the app, even if the primary server is down, but in the browser, again, this code will by itself not link to the fallback server. This is because the QR code only encodes the URL, and cannot encode two URLs at once.

## How to establish a fallback connection

You can find instructions about how to set up a fallback connection on the [wiki page](https://github.com/KL-Psychological-Methodology/ESMira/wiki/Fallback-System#setting-up-a-fallback-server). To summarize, a user with admin access on the primary server needs to acquire a setup token from the designated fallback server. The recommended way for this is to give them an account on the fallback server and give that account the permission to generate such a setup token. They then enter the URL of the fallback server alongside the setup token in the list of outgoing fallback connections on the primary server. This will set up the connection. This connection is unidirectional, so at this point the primary server can use the fallback server as fallback, but not the other way around. To make this relationship bidirectional, simply follow the same procedure with the roles of the servers switched (i.e., an admin on the second server acquires a setup token on the first server, and enters it on the second server).

## How researchers/users/participants will notice the Fallback System

Setting up the fallback system is something that is server-wide, and is done by an admin. If it is set up, researchers will notice it in two places: A checkbox that toggles whether a study uses the fallback system (on by default), and longer/more links and a slightly larger QR code on the publication page of a study. Anything else should work in the background. If something doesn't work, admins will receive an error log on their error logs page. So any changes a regular ESMira user does to a study should automatically be copied to the fallback server upon saving, no extra steps needed.

Users may receive two links, with the instruction to use the second link if the first link does not work. If they receive a QR code and use that to join a study in the app, then the only thing they might notice is a slightly longer loading time in case the app has to use the fallback. This is due to the fact that the app waits a while before it is sure that it won't get a response from the primary server, and only then checks the fallback server. If the connection to the fallback server works, the app has all the necessary information to start the study. If not, then there is nothing more the user or the fallback could do, and things simply don't work (which is already the case if the fallback is necessary). For this reason there is very little feedback about this fallback to app users.

Overall, the user facing part of this system is relatively opaque. The fallback system is only is necessary if the usual process does not work, and if the fallback does not work at that point there is nothing more that can be done. Furthermore, only a server's admins can resolve any issues with connections between servers, so they are the only ones that get the errors. Even if there are issues with the connection, we suspect that displaying them directly when they happen would only lead to false alarms. If a error pops up upon saving a study, users would be unnecessarily worried that their study did not save properly, even when it did, when all that is happening is a problem with the fallback server, while the primary server works as intended.

---

The Fallback System will be available in the next update (3.4.0), for which an alpha version is already available. For more information see the [wiki entry](https://github.com/KL-Psychological-Methodology/ESMira/wiki/Fallback-System) at [https://github.com/KL-Psychological-Methodology/ESMira/wiki/Fallback-System](https://github.com/KL-Psychological-Methodology/ESMira/wiki/Fallback-System).
