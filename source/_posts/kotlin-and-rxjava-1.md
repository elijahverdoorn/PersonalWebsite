---
title: Choosing a Reactive Programming Framework for Modern Android Development 
date: 2019-11-13 14:17:32
tags:
- Java
- Android
- Kotlin
---

The opportunity to participate in the design and development of greenfield applications and systems is, for me, one of the most exciting and energizing engineering challenges that can be undertaken. There is great freedom to be found in the blank canvas, but an empty `main()` function can be quite intimidating at the same time. The sheer number of decisions that must be made early in the development cycle can paralyze skilled developers, even those that are confident in their skills within the codebase that they've become accustomed to. 
Recently in my day-to-day work I've been focused on the creation of new applications, SDKs, and designing for the long-term. In the course of this work I've been finding power in asking questions. Frequently these questions are answered by my colleagues, whose expertise I appreciate and rely on. The questions that I find are most revealing are those that none of my peers can answer immediately, requiring additional research and dedicated study.

A few samples of such questions that I've faced in my recent work include: what frameworks will enable the greatest degree of flexibility while still providing value? What is the best balance between adopting bleeding-edge technology and using tried-and-true solutions? What programming paradigms will be best suited to solving the problem at hand? How will we validate our work? Each of these questions has the potential to spark a long-running investigation before a satisfactory conclusion can be drawn. Spending time on such investigation has led to a great deal of growth for me as an engineer.

One specific area in which I have targeted this growth is reactive, asynchronous programming practices and frameworks for the Android platform. Developers familiar with the Android ecosystem will know that there has been and continues to be a great deal of change in this area: `AsyncTask` will soon be fully deprecated, RxJava is approaching its version 3 release, and the Kotlin language's coroutine implementations are maturing quickly (to name a few). In the course of my research I put together a summary document/blog post comparing a few of the options that exist for developers going forward and published this document on Pandora's engineering blog "Algorithm and Blues". [The post can be found here.](https://engineering.pandora.com/choosing-a-reactive-programming-framework-for-modern-android-development-5280e2924a5a)
An important part of the decision making process in this case was the evaluation of the learning curve for each of the systems being considered. To demonstrate the functionality and provide a set of samples for developers interested in getting a sense of the syntax I also wrote some open-source samples of common use-cases under each of RxJava and Kotlin's structured concurrency (coroutine) model. [This sample code can be found here.](https://github.com/PandoraMedia/recipebook) I'd love to see this project continue to grow and evolve, with the community adding additional samples demonstrating use-cases that I may not have thought of yet!

I look forward to continuing to do this kind of work as I progress in my career and become more involved in the architecture and design process of increasingly large projects.
