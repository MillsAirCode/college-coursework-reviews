# CS-340 Animal Rescue Dashboard

Plotly Dash + MongoDB + Leaflet map. Built for a fictional animal rescue org using the Austin Animal Center dataset. Radio filters for rescue types, paginated data table, breed pie chart, and a map that pins the selected animal. Spring 2025.

The CRUD module in `crud.py` holds up. One method per operation, early input validation, sensible defaults on failure. I still write thin data layers like this for prototypes. The Dash callback architecture is correct too - separate callbacks for table, chart, and map, with the pie chart reading from `derived_virtual_data` so it respects pagination.

The problems are all the "class project" shortcuts. Hardcoded MongoDB creds (`aacuser` / `SNHU1234`) right in the notebook. Rescue type filters are hardcoded breed-to-type mappings baked into the callback with no config. The whole thing is one Jupyter notebook with no `requirements.txt`. The map callback has no null check on coordinates, so missing lat/long crashes the whole dashboard.

**Keep public.** Full-stack wiring that actually works - MongoDB to callbacks to interactive viz. The code is coursework-grade but the architecture is readable and the CRUD module is something I'd actually reuse.
