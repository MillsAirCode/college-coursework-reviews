# CS230-Python

https://github.com/MillsAirCode/CS230-Python

## what it was

SNHU CS-230 (Object-Oriented Programming), spring 2023. A text-based haunted house adventure game in Python. Five interconnected rooms, three keys to collect, a roaming ghost enemy, trap hazards, and an inventory system. All in one file, no external dependencies beyond `random` and `time`.

## what holds up

The room data structure is clean — a dict-of-dicts with consistent keys for description, exits, keys, traps, and items. Easy to extend with new rooms. The `GameState` class actually encapsulates the state, which was the whole point of the CS-230 assignment. The command parser in `main()` is straightforward: split on whitespace, dispatch by first token. Works for a text adventure.

## what I'd refactor

The `use()` function calls `input()` mid-loop, which breaks the main game loop's flow — you get a second prompt inside an already-prompted game state. That's a real bug. The `take()` command only grabs one item per call (the key, not the item), so you need to type `take` twice to get both the key and holy water in the same room. Nobody would figure that out. The global `game` instance defeats the encapsulation the GameState class was supposed to provide. And `move_ghost()` gets called from three different places (move, take, use) instead of once at the end of each turn — copy-paste logic that should be in the main loop.

## portfolio take

Archive. It's a fun little game and the room data model is clean, but the input bug and the global state undermine the OOP lesson the assignment was supposed to teach.
