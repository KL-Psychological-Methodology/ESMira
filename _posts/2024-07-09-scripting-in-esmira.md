---
layout: post
title:  "Scripting in ESMira"
date:   2024-07-09 10:00:00 +0200
categories: feature
author: Selina
---

Over the past weeks I have worked on an interesting package of features: Scripting. ESMira now has its very own scripting language, called Merlin. It is our hope that by integrating this feature package we are providing our users yet more tools to achieve their goals with ESMira.

## What You can do with Scripting

Merlin scripts enable you to execute tiny programs right within ESMira. These programs can be used to decide whether or not to show a particular questionnaire page or item. This decision could be based on responses to other items in the same questionnaire, or even in a previously filled out questionnaire. Thereby you can adapt questionnaires to your participant or the current situation. Similarly, you can use scripts to adapt the item text to the situation, e.g., if you want to provide participants with feedback to the questionnaire they just took. Beyond adapting a questionnaire, scripts can also be useful to simply calculate a value and store it in the dataset. If you need, e.g., the mean and standard deviation of several items in a questionnaire, you can calculate them in a script and have them as part of the dataset. Of course, those values can serve as the basis decisions in other scripts.

As of version 3.3 of ESMira web, studiy configurations feature several places where you can write scripts.

### Scripting End Block

Each questionnaire features a _scripting end block_, which you will find right at the top of the questionnaire configuraiton. Unlike the other blocks, this script will not be evaluated for a value. It will run right at the end of the questionnaire, just before values are saved. This means that when this script runs you can be sure that the questionnaire has been completed, and you may access the responses to any item in the questionnaire. Therefore, this script is a great spot for calculations, and works well with our new alternative to the sum score system. With what we have called _virtual items_ you can calculate values in a script, and then save them so that they are a part of the data set.

### Relevance Scripts

We also introduce what we call _relevance scripts_. Relevance scripts let you selectively hide items or even whole pages. You can find code editors for these scripts when you edit items or pages. Unlike scripting end blocks, relevance scripts are evaluated for a value. When they are run, they result in a truth value that tells the item or page whether or not to display. Note that relevance scripts are only evaluated when they are present, i.e., when the corresponding text field is not empty, so if you don't enter a script the item or page will be displayed as usual. Relevance scripts allow your questionnaires to display a certain degree of adaptability. For example, you might ask a participant on the first page whether or not they have eaten a meal since the last questionnaire. Relevance scripts allow you to have the second page, which asks details about the meal, to only display when they aswer yes to that item on the first page.

### Text Scripts

The last type of script we have for now are _text scripts_. You can find these when editing items, right next to the relevance scripts. Text scripts get evaluated for a string value, and that string value will replace the usual _shown text_. I.e., you can programmatically create item text. Just as with relevance scripts, this will only happen if a script is present, so things work as usual if you don't add a script there. One example of a situation where text scripts can be useful is if you want to provide feedback for your participants within a questionnaire, e.g., the result of the test they just filled out.

### Study-Global Script Variables

Scripts in ESMira need to account for the special context in which they are executed. In contrast to a single script that gets executed a single time, scripts in ESMira are executed across different questionnaires, which may be executed multiple time, in any order. To allow scripts and thereby questionnaires to communicate with each other (and with themself across time), Merlin scripts to store variables[^1] in a globals object that is persistent and accessible from any script within the same study. This allows for many different interesting applications. For example, by starting a variable at 0 and adding 1 every time the script end block is executed, a counter can be implemented (to which other scripts may react). Another example is the calculation of a moving average across multiple days.

[^1]: _Variable_ in this context means a value within a script, not an item in the questionnaire. Script variables only exist within Merlin scripts, not in the collected datasets. However, a variable's value can be filled into a virtual item, thereby transferring it to a value that will be part of the dataset.


## Required Smartphone Versions

Please note for all of this to work, your ESMira server needs to be at least version 3.3 (if you came here via a "news" link in your ESMira admin panel, then your server fulfills that requirement), and the Apps your participants are using need to be on the proper versions as well (Android at least 2.14.3, iOS at least 1.12.5). If a participant freshly installs ESMira for a study this is no problem, but if returning participants use outdated versions of ESMira then some or all of the features outlined here will not work properly, or not work at all.

## What's new in the Admin Panel?

As mentioned above, there are some new properties for scripts on questionnaieres, pages, and items. We have implemented a rudimentary code editor that even does simple parsing of the code to alert you to syntactic errors. At the moment these warning/error messages are very simple, but hopefully will help you see if your code would run at all. If you see an error message and don't know what it means, then it's a good idea to use the old programmer trick to look at the code directly before the error has happened[^2]. We hope that over time we get the chance to make error messages more helpful.

[^2]: This works well because a lot of errors happen because the code so far leads the parser to expect a certain thing to follow, and when it encounters something it doesn't expect, that's when it errors out.

We also mentioned above the introduction of _virtual items_. You can find these under "calculate sum scores". Right next to the old sum score system you can define these virtual items. Virtual items follow the rules of normal items, i.e., they are associated with a certain questionnaire, and their name must be unique among all items (including "normal" items) in the study. Once you have defined a virtual item the dataset will have a column of that name. By themselves virtual items don't do anything, and their value will be empty, unless you fill them with a value in code.

Apart from the study edit section we also have an addition in the data section. You can find a new _script logs_ entry there. Script logs are used for two types of information. First, when the ESMira app encounters an error during executing a script that error will be sent to the server, and you will receive a script log that will hopefully help you to fix the broken script and update your study. The other type of information are what we have called _user logs_[^3]. There's a function you can use within scripts to create such a log. For example, if it's important for you to know when participants respond a certain way to some item, then you can use this system to notify yourself of this (as the interface will highlight new logs, compared to new data in the datasets). This will alert you "silently", as sending logs happens in the background[^4].

[^3]: The user being you in that case, rather than the participant.
[^4]: Participants can see in the upload data that a user log has been sent, but can't see the content of the log.