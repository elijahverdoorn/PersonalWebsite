---
title: My First Contribution to Kotlin
date: 2020-04-25 15:53:29
tags:
---

I'm trapped in quarantine due to the global COVID-19 pandemic. I accept that. I also know that I need to develop


1. Start with the newest version of IntelliJ IDEA. I already had a 2019 version of the Community Edition installed, but the Kotlin project wouldn't build under that configuration. I updated to the latest 2020.1 version of the IDE, I also updated all my plugins. I repeatedly saw build issues around generated code, eventually I resolved these by ensuring that I had downloaded JDK versions 1.6, 1.7, 1.8, and 9; each of these is needed to assemble the project (and don't forget to update your environment variables if you, like me, didn't have some of these legacy versions installed).

2. Import the project. I cloned the main Kotlin repo, opened the project with IntelliJ, and then the waiting game began. It's a big project, so be patient with the first build.

3. Find an area to contribute to! The contributing guidelines directed me towards a preset query that listed a number of issues suitable for new contributors. At the time of writing there was active work to create samples for all the functions avaliable in the standard library, this aligns with my interest in well documented code; I decided to target adding more of these samples as my first contribution.
