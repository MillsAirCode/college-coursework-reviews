# CS-340 Grazioso Salvare Animal Rescue Dashboard

https://github.com/MillsAirCode/CS-340-Grazioso-Salvare-Animal-Rescue-Dashboard

## what it was

I built this for CS-340, spring 2025. Plotly Dash dashboard backed by MongoDB, built for a fictional animal rescue org called Grazioso Salvare using the Austin Animal Center dataset. The dashboard has radio button filters for rescue types, a paginated data table, a breed distribution pie chart, and a Leaflet map that pins a selected animal. The whole thing lives in a Jupyter notebook with a separate crud.py module.

## what holds up

The CRUD module in crud.py is clean for what it is. Each method does one thing, input validation catches bad calls early, and the error handling returns sensible defaults instead of crashing. I'd still write a thin data access layer like this for quick prototypes.

The Dash callback architecture makes sense. Separate callbacks for the table, chart, and map keep concerns isolated. The pie chart updates off `derived_virtual_data` so it reflects pagination and sorting, which is the right choice over reading the full dataset every time.

## what i'd refactor

Hardcoded credentials right in the notebook. `aacuser` and `SNHU1234` sitting in plaintext next to the code. Even environment variables or a `.env` file would be better. This was a class server so it didn't matter at the time, but shipping that pattern to GitHub is a bad habit.

The rescue type filters are hardcoded breed-to-type mappings. Water rescue gets Labradors and Newfoundlands, mountain rescue gets German Shepherds and Malamutes. There's no data-driven way to add or change these -- they're baked into the callback. A config file or a separate collection would make this actually usable.

The whole dashboard is a single Jupyter notebook. Works for a class project, but not something you'd deploy or hand off. I'd split it into a proper Dash app with separate layout and callback files. There's no requirements.txt either -- just a pip install command in the README.

The CRUD class takes username and password in the constructor and opens a connection immediately with no way to close it. No context manager, no connection pooling. For a dashboard that queries once at startup and caches to a DataFrame, it's fine, but the class pretends to be a general-purpose data layer.

The map callback reads `location_lat` and `location_long` with no null check -- if the selected record has missing coordinates, the whole callback crashes. Same with the breed pie chart on records with null breed values.

## portfolio take

Link it. Shows I can wire up a full stack -- MongoDB, Dash, Plotly, Leaflet -- and make interactive callbacks work together. The code is coursework-quality, but the architecture is readable and the CRUD module is genuinely reusable.
