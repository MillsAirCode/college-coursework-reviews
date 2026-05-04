# Weight Tracker Android App

https://github.com/MillsAirCode/Weight-Tracker-Android-App

## what it was

I built this for CS-300, fall 2023. SQLite-backed weight tracker for Android with user auth, CRUD for weight entries, and a chart screen rendered through a WebView. Java, no Kotlin, no Room, no ViewModel -- just Activities and a SQLiteOpenHelper.

## what holds up

DatabaseHelper.java is actually not bad. Parameterized queries everywhere, proper cursor handling with getColumnIndex checks, and a clean schema with a users table and a weight_entries table with a foreign key. I'd still recognize that pattern today.

The login flow with SharedPreferences for session persistence is simple and works. Store the userId after login, check it on every screen. No overengineering.

## what I'd refactor

Java. I'd rewrite this in Kotlin without thinking about it. The anonymous inner classes for onClickListeners in MainActivity are the old way -- view binding or Compose would cut that file in half.

I clearly didn't get the difference between adapter and repository at this point. Every Activity creates its own DatabaseHelper and calls it directly. There's no ViewModel, no repository pattern -- the Activities are doing data access, UI, and navigation all at once. DataDisplayActivity even calls getAllEntries which returns formatted strings instead of WeightEntry objects, so the data layer is leaking presentation decisions.

Passwords stored in plain text in SQLite. I knew better even then -- the README has a "consider encryption in production" disclaimer that basically admits it.

The SMS permission screen is pure filler. It requests SEND_SMS, shows a toast, and does nothing. I just needed another Activity to check a rubric box.

ChartActivity builds JSON by hand with StringBuilder string concatenation instead of using Gson, which is literally in the dependencies. The chart.html file from assets isn't even in the repo. RecyclerView is in the build.gradle but I used ListView anyway.

## portfolio take

Keep it. Shows a solid understanding of Android fundamentals -- SQLite, SharedPreferences, WebView, runtime permissions -- even if the architecture is flat. Good artifact for "early Android work" on a resume.
