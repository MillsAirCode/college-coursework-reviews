# CS230 Haunted House

Text adventure in Python. Five rooms, three keys, a roaming ghost, traps, inventory system. One file, no dependencies beyond `random` and `time`. CS-230 OOP assignment.

The room data model is good - dict-of-dicts with consistent keys for description, exits, keys, traps, items. Easy to extend. The `GameState` class actually encapsulates state, which was the point.

But it has a real bug: `use()` calls `input()` mid-loop, so you get prompted inside an already-prompted game state. The `take` command only grabs one item per call, meaning you type `take` twice in the same room and nobody would guess that. The global `game` instance defeats the encapsulation the class was supposed to demonstrate. And `move_ghost()` gets called from three separate places instead of once at the end of each turn.

**Archive.** Fun to write, clean data model, broken interaction loop.
