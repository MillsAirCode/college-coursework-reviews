# SNHU Travel

Express + Handlebars with static HTML from a freewebsitetemplates.com beach resort theme bolted on. The controllers are stubs - `res.render('travel', { title: 'Travlr Getaways' })`. No database, no auth, no booking logic.

The Express project structure is fine (express-generator pattern), and the Handlebars partials setup is clean. That's where the positives end.

The static HTML files at the root aren't even served by the Express app. There's a `extendxed: false` typo breaking urlencoded parsing. The users route literally says "respond with a resource." I clearly rushed this to meet a deadline without connecting anything to anything.

**Archive.** Express skeleton with no backend. I can set up a Node project, which isn't exactly a differentiator at this point.
