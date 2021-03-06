---
title: Projects
date: 2017-07-08 23:14:34
---

# Active

These are projects that I'm currently working on in some capacity - they may be available to the public, they may still be in development, but in either case I'm committed to maintaining them. Source code for most of these projects can be found on my [GitHub](https://github.com/elijahverdoorn/), I'd love to take on new collaborators or just receive feedback on my work.

## Duplicate Tab Hotkey

Configuring and customizing my development setup to optimize productivity is a hobby of mine, one which contributes not only to my own enjoyment of my work but also to the rate at which I can accomplish tasks. Many of the tools that I rely on support an extremely high degree of customizability: terminals emulators, IDEs, and text editors are all designed with an infinite variety of workflows in mind; they tend to support more than enough customizability out-of-the-box. Some tools that I use frequently, however, do not share the same philosophy regarding customization: namely Google Chrome. For as much as I rely on the browser it does not natively support nearly the degree of freedom that I'd like. There exist browser extensions which serve to fill in some of the gaps, but many of these extensions request permission to read and modify data on the sites that one visits, or generally track users in ways that I'm not comfortable with. Out of concern for personal privacy and security I have refrained from installing such extensions. I do, however, desire some of the functionality that they provide; to support one of my most wanted features I created and published my own extension that simply adds the ability to duplicate a tab with a hotkey: a feature that is surprisingly missing from the base application. This extension is open source and can be downloaded from the [Chrome Web Store](https://chrome.google.com/webstore/detail/duplicate-tab-hotkey/adgkgjklgiilebgjckenkknhbenpiinc), or compiled from [source](https://github.com/elijahverdoorn/duplicate-tab-extension) and manually loaded into the browser.

## Chrono Daily Deal

Continuing to explore my interest in the Actions on Google platform, I decided to automate one of my daily routines - checking the latest video game deal available on [chrono.gg](https://chrono.gg). This retailer's gimmick in the crowded game market is to sell a single game at a time, at discount, rotating the selection daily at 9AM. I'd gotten in the habit of checking out the deal on a near daily basis, sometimes finding a steep discount on a game that I'd had my eye on. To make this daily routine easier I built and published "Chrono Daily Deal", an action for the Google Assistant that can tell you what game is on sale and the price of said game. This action is live in production, to try it for yourself just ask the Google Assistant to "talk to Chrono Daily Deal". If, after trying it, you're interested in seeing the source code backing it you can check that out on my GitHub.

## Recipebook

Through my work in the Android development space I have become increasingly interested in the Kotlin programming language, specifically how the language handles background computation and reactive patterns via it's coroutine system. After becoming a go-to person on Pandora's android team for questions about both the coroutine system and how it compared to the more familiar RxJava library I began development of a set of examples that compared how to accomplish common tasks under both the native structured concurrency model and within RxJava's framework. My teammates at Pandora appreciated the samples and used them for reference, so I worked with the legal department to open-source these samples. While I no longer am the maintainer of this codebase due to not being a Pandora employee, I remain an occasional contributor to the repository.

## Keep Score

Keep Score is a Actions on Google & DialogFlow project that began as a hackathon exploration of the capabilities of the Actions platform. In just three days I implemented an agent that demonstrated the basics of conversation; expansion of these capabilities over time became a side project that has been important in keeping my JavaScript skills sharp. Code for this project can be found on my GitHub. This action is currently in beta, if you're interested in seeing the capabilities in action feel free to get in contact; I'd welcome more testers!

---

# Past

There comes a point in every project life cycle when it is time to move on. Projects listed here are ones from my past that I'm proud of, but am not currently working on. These projects may be ongoing under new management, or they may be sun setted and unsupported.

## All About Olaf

Development on All About Olaf began about a year before I took over the project, but I quickly realized that the native iOS application needed a complete rewrite. The first move I made to meet the deadline presented of September 2016 after beginning the project in May of the same year was to adopt React Native, enabling rapid cross-platform native development for both iOS and Android using JavaScript. From there, the application's development was a learning experience into the React ecosystem, which I have remained interested in. Still being updated after an on-time release, the application is open-source and has been installed by 50% of the students on St. Olaf's campus. 

## Oleville

Oleville is the website of the St. Olaf College Student Government Association, and it's development was a large part of my college career. I joined the team of developers building the site in my first semester at St. Olaf, and during my junior year had the honor of leading that team as the Chief Technology Officer. Oleville is built on WordPress, and uses a custom theme developed in-house for maximum flexibility. Management of the site has given me exposure into release management, database management, system administration, and user education.

#### Members

Members is a plugin developed for Oleville that allows administrators to feature all the members of their organization on Oleville. As my first exposure to plugin development, this process taught me about the basics of WordPress, database usage, and the PHP programming language.

#### Voting

The Voting plugin was built to facilitate the need for a robust system with which to manage student government elections. The plugin was my first experience integrating LDAP for user login, and has been modified heavily since the first iteration, which was put into practice on the spring of 2015. Development and maintenance of this plugin gave me the opportunity to reflect numerous times on the code that I had written in the past and make improvements, which has been a good chance to right past mistakes and become deeply familiar with not only the code but also the problem area.

---

# Past Academic

A few projects stand out from my academic history, these are listed here but are not necessarily representative of my current work capacity; I keep them noted on this page because they were significant milestones for me as I grew as a developer. I learned a lot from completing them, but don't have plans to expand on the work I've done in these areas at this time.

## Web Rendering of 3D Models

During January 2016 I led a team of undergraduates in a research project that focused on devising novel ways to render complex 3D models on the web. This application is a part of a set of larger research that aims to create a 3D model of the interior of the science center on my campus from nothing but a set of images, no measurements allowed. The constraints given present unique challenges that enable student exploration of areas of computing that might not be traditionally taught in the classroom. Companion projects included color correction, semantic segmentation of small image datasets, and stereoscopic rendering.

## Turing Machine Simulator

As a final project for my Theory of Computation class, I built a simple simulator of turing machines using JavaScript. The application was developed quickly, but was successful and demonstrated my ability to develop on the web in an academic setting.

