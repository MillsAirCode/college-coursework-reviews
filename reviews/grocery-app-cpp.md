# GroceryApp
https://github.com/MillsAirCode/GroceryApp

## what it was

SNHU coursework. A C++ console application that tracks grocery item purchase frequency — you'd add items to a list and the program would count how many times each item appeared, then display a sorted frequency report. Simple data structures exercise, probably C++230 or a similar intro-to-intermediate class. All console I/O, no GUI, no external dependencies.

The repo is deleted now (404 on GitHub, no Wayback snapshot), so this review is based on the project description and the pattern of SNHU C++ assignments from that period.

## what holds up

The core idea is solid — a frequency counter is a natural fit for a `std::map<std::string, int>` or `std::unordered_map`. That's basically the first useful data structure you learn in C++ after arrays. The console-based approach was appropriate for the level; no need to over-engineer a GUI for a counting exercise. The sorted output requirement (showing items by frequency) is a good lesson in `std::sort` or iterating a map in reverse order.

## what I'd refactor

If this was a single `main.cpp` with everything in one file, split it out. Header/source separation was probably taught by then, and a 500-line main with embedded parsing logic doesn't teach good habits. I'd also replace the raw `std::map` with a proper `Item` struct (name, count, maybe category) and use a `std::vector<Item>` with a custom comparator for sorting — that's the kind of pattern that shows up in real code and makes the transition to more complex projects smoother.

The input parsing is almost certainly the weak point. Console grocery apps tend to have fragile input handling — no validation, no way to handle typos, maybe a broken "quit" command that doesn't flush buffers. If it was built like the other SNHU C++ projects from that era, I'd bet there was at least one `cin >>` that left a newline in the buffer and broke the next `getline()`. Classic.

## portfolio take

Archive. The frequency-counting concept is clean and the map-based approach is defensible, but a console grocery tracker doesn't show much beyond "I can use std::map." It's fine as coursework. Not worth keeping as a portfolio piece when there are more interesting projects in the archive.
