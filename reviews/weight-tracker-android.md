# Weight Tracker (Android)

Java Android app with SQLite, SharedPreferences for sessions, a WebView chart, and the usual CRUD. Built for CS-300, fall 2023.

The DatabaseHelper is genuinely decent. Parameterized queries, proper cursor handling, `getColumnIndex` checks, clean schema with a foreign key between users and weight entries. I'd recognize that pattern today.

Everything else is rough. Every Activity creates its own DatabaseHelper and hits the DB directly - no ViewModel, no repository pattern, no separation at all. `DataDisplayActivity` returns formatted strings from the data layer, leaking presentation into what should be a model concern. Passwords in plaintext SQLite with a "consider encryption in production" disclaimer that basically admits I knew better. The SMS permission screen requests `SEND_SMS`, shows a toast, and does absolutely nothing - I needed another Activity to check a rubric box.

The chart is built by hand-concatenating JSON with StringBuilder instead of using Gson, which was already in the dependencies. And the `chart.html` asset file isn't even in the repo.

I'd rewrite it in Kotlin without thinking about it.

**Keep.** Flat architecture aside, it demonstrates Android fundamentals end-to-end. Shows I was building real apps, not just following tutorials.
