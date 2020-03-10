---
title: Picking Up Pennies
date: 2020-03-03 14:04:11
tags:
---

![Penny](penny.jpg)

According to the step-tracker built into my phone, thus far in 2020 I have walked, on average, 7.16 miles per day. This is, of course, just a rough estimate, but it seems reasonable to me: I walk about 2 miles every morning to catch a train to the office, and about a mile and a half at night to return to my apartment; I also take a daily walking break at lunch to clear my head and get some fresh air; factoring in the rest of my daily steps around the office, errands, and general activity I can accept 7.16 as a ballpark estimate. Given the distance, this clearly takes a good chunk of time in my day - I fill this time by consuming _a lot_ of audio entertainment: music, podcasts, and audiobooks are staples in my media diet.

#### A Few Top-of-Mind Audio Entertainment Recommendations
<br>

<style type="text/css">
.tg  {
	border-collapse:collapse;
	border-spacing:0;
	width:100%;
}
.tg td{
	padding:10px 10px;
	overflow:hidden;
	word-break:normal;
}
.tg th{
	padding:10px 10px;
	overflow:hidden;
	word-break:normal;
}
.tg .tg-0pky{
	border-color:inherit;
	text-align:left;
	vertical-align:top;
}
</style>
<table class="tg">
  <tr>
    <th class="tg-0pky">Podcasts</th>
    <th class="tg-0pky">Music</th>
    <th class="tg-0pky">Audiobooks</th>
  </tr>
  <tr>
    <td class="tg-0pky">The NPR Politics Podcast<br>Up First<br>The West Wing Weekly<br>Work For Change<br>Stronger by Science<br>The WAN Show Podcast</td>
    <td class="tg-0pky">Lord Huron<br>Iron and Wine<br>Dessa<br>Doomtree<br>CRSB<br>Monakr<br>Sabaton</td>
    <td class="tg-0pky">Atomic Habits, <i>James Clear</i><br>The Power of Habit, <i>Charles Duhigg</i><br>Freakonomics, <i>Stephen J. Dubner and Steven Levitt</i><br>Harry Potter, <i>J. K. Rowling</i><br>The Lord of the Rings, <i>J. R. R. Tolkien</i><br>My Own Devices, <i>Dessa</i></td>
  </tr>
</table>

As much as I enjoy all of the above content (and that's just a small sample!), I find that I sometimes prefer to simply walk in silence: observing the world around me, those that I pass on the street, and listening to the sounds of the city. It is in these moments that I find a great deal of mental clarity, frequently coming up with solutions to longstanding problems, making progress towards my self-reflection goals, and taking general inventory of my life. I encourage any and everyone who is stressed or feeling overwhelmed to try going for a walk, especially if it's not a regular part of your life: you may find the practice helpful.

While the mental benefits remain the primary driver that gets me to lace up my walking shoes every day, I have also found that it saves me a good deal of money: I don't need to pay for a car and the associated parking, fuel, and repair bills, nor do I spend as much on rideshares as I once did. In fact, I've probably *made* money by walking: the amount of loose change that I find on the sidewalk is astounding. In the past week alone I've picked up a coin on every walk I've been on. These coins are mostly pennies, so their overall value is small in the grand scheme of my financial life, but nonetheless I enjoy picking them up. On a recent outing, after spotting a dime ahead, I was bending down to claim my bounty when a thought came over me: "What can be learned from picking up this change? There's got to to be a lesson here somewhere!". Being a lover of metaphor and analogy, and always seeking blog post ideas, I quickly found the idea of picking up change to be connected to how I think of making small changes "along the way" to an unrelated goal.

I never set out on a walk with the intention of finding money, it is just a positive side-effect of something that I'm already committed to doing. I find this same principal surfaces in my day-to-day engineering work. Let's say, for example, that I am working on implementing a new feature into an app. In the course of accomplishing the tasks that will add up to the feature being released to our users I'll occasionally happen across a small change to an unrelated system that I can make easily, thereby improving the health of the project as a whole. I'll make the micro-improvement and include the change as a part of the implementation effort towards the feature work that is my ultimate goal.
These small auxiliary changes are miniscule in size compared to the feature that I'm focused on but over time they do add up, much like picking up change on the sidewalk will eventually result in a full piggy-bank! Unfortunately on a few occasions after submitting work for review containing changes in this vein I've received surprisingly negative feedback on my penny-sized advancements. Reviewers complain that the inclusion of these changes contributes to clutter, that all changes ought to be associated with tickets in task-tracking software, and that such modifications are "out of scope" from the items of work primarily targeted by my patch. In response I'd say that while I didn't set out to correct spelling errors in comments, I didn't intend on happening across unused `import` statements, and I wasn't hunting for mis-formatted braces I'm only taking advantage of being in the right place at the right time! Much like neglecting to put in the effort to pick up a penny on the sidewalk because "it's only a penny" feels elitist and entitled I'd feel like a poor steward of quality were I to simply ignore an obviously positive change I could make to code as I passed by. 

These tiny, nearly imperceptible improvements add up over time to a codebase that is, at the end of the day, more pleasant to work on. Fixing spelling errors leads to better search results. Improving compliance to our styleguides makes our continuous integration system less likely to fail. Removing unused `import` statements increases the isolation of individual product areas and can create opportunities to deprecate dependencies entirely over time. The benefits of making these tiny improvements are hard to observe in the short term, just like we may struggle to see the spare-change jar getting any more full every time we deposit the day's spoils, but that shouldn't deter us from doing it anyway with the knowledge that we'll thank ourselves the day that we finally get to take the contents of that jar to the bank to be counted. In my opinion we shouldn't let task-trackers, processes, and "feature scope" get in the way of us individually doing what we know is best. Just like that rewarding trip to the bank we'll thank ourselves the next time we `grep` our code in search of a specific method, the next time our CI builds pass under style-violation thresholds, and reap the architectural benefits of separation of concerns.

In closing, I'd recommend that the next time you face a challenging problem you take a walk, and if you find a bit of spare change along the way be sure to pick it up: it'll add up to something big over time.
