---
title: My Kotlin Toolbelt
date: 2020-03-28 16:15:34
tags:
---

Adopting Kotlin as my primary development language has been a great experience, improving my day-to-day satisfaction in my professional work developing Android apps and increasing my motivation to further my skills in my spare time. Having a language that provides a concrete foundation upon which to build is critical, but it's the community developments that spring up on top of that foundation that either keep me coming back to a language or drive me away to explore other options. Kotlin's community and auxiliary packages continue to impress me, below are a few of the libraries that I rely on and would encourage developers to check out, no matter where you are in your Kotlin journey.

### IDE

Daily development in Kotlin is greatly improved by the deeply integrated support for the language found in JetBrains IDEs. IntelliJ (and Android Studio, which is derived from the same set of base features) is a powerful tool to begin with for developing on the JVM, but its potency is only increased when used with Kotlin. I'm most thankful for the consistent support that new language features receive in the IDE, with the Kotlin plugin often receiving updates on the same day as new language versions are released. Little niceties like an inline icon showing the start of asynchronous blocks of code, debugging support for Coroutines, breakpoints and inspection tools that interact cleanly with all features of the language, and more all point to a language development team that keeps the day-to-day experience of developers using the language in mind throughout the process of building and molding the Kotlin ecosystem.

### Coroutines

One of the most exciting features of Kotlin is it's support for Coroutines. Hundreds of blog posts exist to introduce, teach, and deep-dive in to every corner of the coroutines APIs, but I've become enamored with them as a means of easily wrangling work that would once have been challenging. API calls, heavy computation, database reads and writes, and file operations are all made much simpler 

### MockK

I'll be the first to admit that testing code isn't always the most thrilling part of the development process. I know and preach it's importance, I advocate for continuously increasing code coverage and test stability, and . Still, sometimes walking the walk isn't as fun as talking the talk, testing is one of those areas for me. In past codebases I'd mostly relied on Mockito to make testing less painful, but in recent work I've changed my tune and have begun using MockK instead. While Mockito does have a supporting library that provides some nice Kotlin sugar, MockK has been developed from the ground up for Kotlin. As a mocking framework it is remarkably intuitive and covers everything that one would need: mocking of suspending asynchronous code, static mocks, spies, and even Kotlin's extension functions. Even as an experienced developer it still makes me smile when code reads in a way that a non-programmer could understand, MockK does this frequently. An example:

```
fun `My Test`() {
	val myString = "Hello, World!"
	val mockedClass = mockk<Class>()
	every { mockedClass.someFunction() } returns myString

	// ...
}
```

### Ktlint

All codebases are improved by being consistently formatted. Enforcing a set of standards for all members of a development team to follow is made easy when you have unbiased tools holding everyone accountable. Almost all languages have tools to do this; ktlint is my go-to for Kotlin formatting. It's easy to adopt, since it takes no special configuration and bases its standard rules on the official code style recommendations established by the language development team. It integrates cleanly with Android build systems (Gradle, namely), has a built-in formatter to fix simple problems without developer intervention needed, and is fully customizable in the case that you need to make modifications to the strong base that it comes with.

### Detekt

If one format and style analysis tool is good, then two can only be better, right? Detekt is similar to ktlint, seeking to enforce a set of standards on a codebase. It is similarly easy to get started with, has a equally simple configuration process, and a set of defaults that are sane and non-offensive to most experienced Kotlin developers. I've found success with running ktlint and detekt in parallel on the same codebase, so you don't have to choose between the two.

### Koin

Dependency injection makes Object Oriented Programming manageable. As I was first learning to write code in high school I was taught Java. At the time I wasn't developing anything significant, no application with more than a few classes, but I still sometime felt that the construction of objects in the places where they were needed was an arduous task. I didn't know any better at the time and assumed that my struggles were a result of my inexperience, I now know that I'd begun to run up against the issues that DI was designed to solve. There exist many Kotlin libraries to support dependency injection (not that any of them are necessary, I've had great success with establishing manual DI patterns with my own interfaces and factories), but my personal favorite is Koin. It's lightweight, has support for Android and Android Jetpack libraries, and takes the least amount of boilerplate code of any DI framework I've used to date.

In order to keep growing as a Kotlin developer I know that I need to keep exploring new ways to get things done, exploring emerging libraries has been a great way to expose myself to novel ideas and challenge what I believe to be the "best" way. To that end, readers can contribute to my development: what are your favorite Kotlin tools, libraries, and ideas? How have you improved your day-to-day development with Kotlin?
