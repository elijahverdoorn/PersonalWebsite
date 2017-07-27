---
title: Senior Days Trivia Game Retrospective
date: 2017-07-10 21:56:49
thumbnail: seniordayslogo.png
---

![Senior Days Logo 2017](seniordayslogo.png)

# Background

At St. Olaf, the Student Government Association has a tradition of hosting Senior Days, a three day series of events for senior students after second semester final exams but before graduation exercises. The events differ each year depending on the organizers, who are always non-senior students. I've been working senior days as a assistant organizer for the last few years, and this year was asked to coordinate one evening's events, a trivia night reminiscent of classic bar trivia. I was honored to be asked to lead this event, and decided that the best thing to do would be to emulate some of the systems that I'd seen in use at restaurants and bars that I've been to and make a digital trivia system. How hard could it be?

I was given rather little time to design and implement a system, having been given my project just two weeks before the event was to be held, in the middle of the final exam season. With looming exams, the project was pushed off to the side in favor of passing classes. Once the semester was finally winding down I found myself tired, but with a trivia system to build.

# Tech Stack

I knew that I had to pick technologies that I had experience with, I didn't have time to develop the system and learn new things at the same time. I've been bitten by the Node.js bug and have a good amount of experience with it, so I knew that whatever I was going to make would use Node for the server; I ended up adding Express for familiarity. I expected the event to be outside on the campus quad, so I planned for most of the interaction to be on cell phones. I could have done a native mobile app, or done it cross-platform with React Native, all of which I've done before, but I didn't want to risk running into issues publishing the apps on the respective stores, so I settled on a simple web client and just kept in mind that most interaction would be on mobile. I then knew I needed to pick a front-end framework (or choose to skip using one). I have used React before, so that was on the table, but given the simplicity of the UI and the rapid development, I decided that React was more than I needed and used Pug templates, which are the default that come with Express. I made these decisions the morning I started seriously working on the project during my morning shower, but despite the rapid choices I wasn't ever disappointed.

A bit more time was put into the database decision, which was really what the application ended up being about. I knew that the majority of this system would be a glorified CRUD application, so I wanted to pick my database carefully. I'm sure that there are a million good solutions, but I was restricting myself to systems that I'd used in the past, so that left me with a limited set of choices. I quickly settled on a SQL database, since I have the most experience with SQL systems and believe that, with few exceptions, almost all data is structured. From all the sQL database implementations, which one did I want to use? I ruled out anything heavy, as I didn't need performance - I expected to have at most 120 questions in the database, with at most 5 answers each, for at most 500 teams. Any modern database can handle selecting, joining, and updating data of that size. I wanted a single server solution that would require very little set up time, so I went with SQLite 3, which I've used extensively on Android, but never on the server side. I am pleased to say that it worked like a charm. I still have yet to find a CSS framework that I like (and generally feel uncomfortable with CSS in general, if I'm honest), so I went with the flavor-of-the-month Mini.CSS.

To summarize, I ended up with:

- SQLite 3
- Node.Js
- Express
- Pug Templates
- Mini.CSS

# Development

Starting any new project is intimidating, but I didn't have much time to waste, so I set out to build a stable sever solution, thinking that I could build my client out later. This turned out to be a good method, but left one fatal flaw to be discussed later. I got my database set up quickly, and found that the fastest way of working with it was to just write an `init.sql` script that I could run after deleting the entire database if I made a mistake. While this may seem ridiculous to some, and it is for any real production system, remember that there were no users for my product for it's entire development cycle, and that the data only needed to exist for a few hours during the actual event. While there are many more sophisticated solutions, this method worked for me since SQLite can create databases instantly and doesn't need to be run in a separate process from my web server. 

## `init.sql`
```
-- Init script
-- Create tables for Senior Days Quiz Game
-- Elijah Verdoorn, May 2017

CREATE TABLE teams (
	id INTEGER PRIMARY KEY ASC,
	name VARCHAR NOT NULL,
	points INTEGER
);

CREATE TABLE question (
	id INTEGER PRIMARY KEY ASC,
	category_id INTEGER,
	question VARCHAR,
	used INTEGER,
	points INTEGER,
	FOREIGN KEY(category_id) REFERENCES category(id)
);

CREATE TABLE category (
	id INTEGER PRIMARY KEY ASC,
	text VARCHAR
);

CREATE TABLE choice (
	id INTEGER PRIMARY KEY ASC,
	question_id INTEGER,
	choice VARCHAR,
	correct INTEGER,
	FOREIGN KEY(question_id) REFERENCES question(id)
);
```

Once I had my database schema decided on, I got to work accessing it through the web server, which turned out to be really simple given the `sqlite` package, all I had to do was
```
// make connection to SQLite3 and start server
Promise.resolve().then(() => db.open('./db/database.db', {Promise}))
		.catch(err => console.error(err.stack))
		.finally(() => app.listen(3000))
```
at the end of my `index.js` file. Sweet, database connection done - might not be secure, might not be fast, might not be scalable, but it'll work for my purposes.


I won't belabor the entire process, but it turned out to be really simple and ended up being less than 200 lines of JavaScript to get the server done. I'll admit that it took me a bit longer than I'd like given the simplicity, but I'm happy overall with my server solution. Given more time, it could use more attention to security (there's some definite potential for session hijacking and SQL injection in there), more thought to the error handling, and the whole thing could be split up into a few more files to avoid the monolith that I have now.

Front end development came together pretty quickly, after grabbing the `mini.css` package from NPM it was a simple matter of making the templates look as good as I could given the time remaining, then sourcing questions. Once I was happy with the look and feel I spun up a quick droplet on DigitalOcean and got my code deployed. I ran some quick manual tests on a few different devices (remember, this is a mobile-first site) and set out to replace the testing data in my database with real questions. This is where the aforementioned fatal error comes in - I had failed to define any simple way to insert questions into the database. This realization came with one hour to go until the event. Mortified, I made the assumption that I didn't have time to code up a solution, but would be better off trying to make one big SQL script that would fill the database with all the questions. A quick search yielded a good plain text file of trivia questions, so I set out to transform the file into a valid SQL script. This decision, combined with the initial error of forgetting to solve the problem in the first place, spelled doom for the system. I became quickly nervous, flustered, and was unable to get a working SQL script done in time for the event. I had a trivia system, but no questions for it to ask.

# Crisis Management

What could have been done at the point of realizing my mistake that may have changed the outcome?

1. I could have trusted myself, and written the code. A quick, non-styled question creation page that would take a form and put it in the database. Would have been easy. Deploy the new version, then get some of the other workers to help me insert the questions. I only needed 100 or so questions, and could have been inserting them as the event happened if need be. This option, in retrospect, would have been the smartest choice, but in the moment didn't make the connection.
2. I could have prepared a SQL query, and inserted one question at a time by copy/paste into the statement. I'm pretty fast with a mouse and keyboard (and vim!) and could have gotten at least a question a minute inserted, probably more. This would have been fewer questions ready than the previous option but would have ensured that I wasn't hit-or-miss, that wherever I got to before the event started would have been useful rather than being caught halfway done with the task and nothing to show for it.
3. I could have immediately scrapped the entire project, and prepared to do the event without a digital system. This solution may seem radical and non-productive, but it must be remembered that the goal was not to engineer a trivia system, but to hold a trivia event. Nothing says that I had to write a single line of code, I just chose to do so because I had a vision and the skills to make it happen. This choice would have led to an event that was not what I dreamed of, but would have been more prepared.

Any of the above would have resulted in more than what I ended up with. I let panic get the better of me, stopped thinking, and tried to brute-force my way through a problem out of frustration. This never works, and I hope to remember this in the future when I find myself in a similar situation.

While having thoughts about what to do in these crisis situations is necessary, we all hope to never reach that point, which of course makes me question what I could have done to remember to build out a question insert mechanism from the start. Would formally defining requirement have helped me? Did I think of it, but never build it? If so, I could have used a task-tracking system to make sure I got everything done, even a bunch of post-its would have worked. My theory is that talking it out with another person, preferably another engineer, would have saved me this mess. Another engineer would have asked me questions, made me think more, and perhaps catch the issue. Another point for collaboration, not that anyone needed reminding of the importance of teamwork.

# The Event

So, how did it turn out? To my surprise, it went _really_ well. Attendance was high and with seconds until the event I scrounged up last year's questions in spreadsheet format, grabbed that microphone that some of my coworkers had kindly set up after seeing me in a panic, and hosted trivia completely improvised. Running the game as fill-in-the-blank or just open-answer kept me from having to make up choices on the fly, grabbing someone with a notepad to help me keep score made it possible for me to engage attendees in dialogue and made the entire thing more personal, and with a little attention to time management I was able to hold the event to the time given to me with little issue. 

Was it a total engineering failure? Yes. Was I disappointed? For sure. Would I do my development the same way again? Not a chance. Did the seniors have a good time, walk away smiling and happy? Yup, and that's all that matters at the end of the day.

[*All code discussed here is availiable on GitHub.*](https://github.com/oleville/senior-days-trivia)
