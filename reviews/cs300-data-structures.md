# CS300

https://github.com/MillsAirCode/CS300

## what it was

C++ data structures project for CS-300 at SNHU. The assignment was to design a course catalog system that stores and retrieves course information using three different data structures: a Hash Table, a Vector, and a Binary Search Tree. Each structure gets its own `loadCourses` and `printCourseInformation` implementation. The repo is pseudocode only -- no actual compiled code, just a Word doc with the designs and a README.

## what holds up

The Course struct (courseId, name, prerequisite) is a clean domain model for the problem. Simple, no overengineering. Separating the load and print logic per data structure makes the comparison between approaches visible, which was the whole point of the assignment.

The Hash Table design with chaining (setting key to UINT_MAX and linking via next pointer) is a reasonable collision strategy. Not the prettiest, but it works and shows I understood the concept.

## what I'd refactor

The README reads like it was run through a thesaurus -- "delved into inherent advantages", "refined my perspective", "illuminated my non-intuitive approach to recursive thinking". I would never write like that in a real project. It sounds like I was trying to hit a rubric word count.

The pseudocode has some rough edges. The `prereq .` syntax in the CSV parsing is unclear -- looks like a typo that never got cleaned up. The Hash Table insert logic mixes collision handling and empty-slot detection in a way that's hard to follow. A separate `findSlot` helper would make it readable.

No actual implementation to test against. Pseudocode is fine for a design doc, but without compiled code or even a test CSV, there's no way to verify the BST insertion or hash collisions actually work. I clearly treated this as a write-up exercise rather than building something runnable.

## portfolio take

Archive it. It's a design exercise, not a shipped project. The pseudocode shows I understood the three structures at a surface level, but there's nothing here that demonstrates actual engineering skill.
