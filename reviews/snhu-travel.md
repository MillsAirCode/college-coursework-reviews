# SNHU-Travel

https://github.com/MillsAirCode/SNHU-Travel

## what it was

I built this for a full-stack web development class at SNHU around 2023. The assignment was to make a travel booking site using a MEAN/MERN-style stack. What I actually shipped is an Express server with Handlebars templates sitting next to a bunch of static HTML pages ripped from a freewebsitetemplates.com beach resort theme. The Express routes render views, but the controllers are basically stubs -- `res.render('travel', { title: 'Travlr Getaways' })`. No database, no auth, no actual booking logic.

## what holds up

The Express project structure is fine -- `app.js` sets up middleware, routes are in their own files, controllers are separated from routes. That's the express-generator pattern and it's still a sensible default. The Handlebars partials setup (header, footer registered with `hbs.registerPartials`) is a clean way to DRY up templates.

## what I'd refactor

This is almost entirely a static template with an Express skeleton bolted on. The HTML files at the root (index.html, travel.html, etc.) are never actually served by the Express app -- they're just sitting there. The `public/` directory has duplicates. The `extendxed: false` typo in `app.js` line 25 means `urlencoded` parsing is broken. The users route is a placeholder that says "respond with a resource." I clearly rushed this to meet a deadline without actually connecting the backend to anything. I'd start over with a proper data model, seed some travel destinations in a database, and wire the routes to actually query and display data instead of hardcoding lorem ipsum in templates.

## portfolio take

Archive it. It shows I can set up an Express project, but it doesn't demonstrate anything I couldn't do better now without thinking about it.
