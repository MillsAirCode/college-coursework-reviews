# CS-230: Top 5 Destination List

[https://github.com/MillsAirCode/CS-230](https://github.com/MillsAirCode/CS-230)

## what it was

A simple Java Swing desktop application designed to display a list of five travel destinations. It features a custom `JList` renderer that combines text with icons and uses a `MouseListener` to launch URLs in the user's default web browser when a list item is clicked.

## what holds up

*   The `TextAndIconListCellRenderer` is a solid implementation of the `ListCellRenderer` interface. It correctly handles the `isSelected` state, ensuring the UI provides clear visual feedback when a user interacts with the list.
*   Proper threading: Using `SwingUtilities.invokeLater` shows an understanding of the single-threaded nature of Swing and ensures the UI is initialized on the Event Dispatch Thread.

## what I'd refactor

*   The data model is essentially hardcoded into the `Destinations` class. I'd extract that into a separate configuration file (like JSON or XML) or a database to make the list dynamic and easier to maintain.
*   The `selectPackageListener` method is a bit clunky. I'd implement a cleaner command pattern or at least move the `MouseListener` logic into its own dedicated class instead of an anonymous inner class to improve readability.
*   Error handling in the mouse listener is too basic—just a `printStackTrace()`. I'd add proper logging or user-facing alerts if the URL fails to open.

## portfolio take

Keep: A basic, clear example of Swing UI customization for a portfolio.
