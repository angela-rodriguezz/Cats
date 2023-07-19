# Cats

<img src="./cats-type.gif">

Inspired by the website [typeracer](https://play.typeracer.com/), this is a program measuring typing speed that implements typing autocorrect. This feature attempts to correct the spelling of the word after a user types it. 

## cats.py File

In this file, I implemented functions which chose the paragraphs users type the [data](data) folder. Given a list of paragraphs 
- a `select` function returning True for selectable paragraphs, and some index `k`. This returns the kth paragraph where select returns True or returns an empty string if no paragraph exists due to a large k.
- an `about` function taking a list of `topic` words and returns a function taking a paragraph andd returning a boolean of if this paragraph has any words in topic. Used for passsing the returned function to choose as select argument.
- an `accuracy` function taking a `typed` paragraph and `reference` paragraph to return the percentage of words in typed that match exactly to words in reference, including case and punctuation. If typed > reference than all extra words are incorrect. Else if both sets are empty then the accuracy is 100%. Else if one set is empty and the other is not, accuracy is 0%.
- a `wpm` function to compute words per minute given string `typed` and `elapsed` time in seconds.
- an `autocorrect` function taking a `typed_word`, a `word_list`, a `diff_function`, and a `limit`. If this typed_word is in word_list, then this word is returned. Otherwise the most similarly spelled word in word_list is returned. Else if the most similar word has a difference in speling > limit typed_word is returned.
- a `sphinx_swaps` function for taking two strings and returning the minimum number of characters to be changed in the `start` word to transform it to `goal` word.
- a `minimum_mewtations` function that returns the minimum number of edit operations needed to transform the `start` word to `goal` word.

## cats_gui.py File

This is the file where I implement the multiplayer functionality so if connects to the course server cats.cs61a.org and looks for someone else to race against. There are 5 different programs running including the GUI for text coloring/display on web browser, the cats_gui.py web server that communicates with the GUI, the opponents GUI and cats_gui.py, and the CS 61A multiplayer server which matches these players. While typing, the GUI uploads your typed words into the cats_gui.py server, returns a progress update, and uploads this update to the multiplayer server.
- a `report_progress function` to call every time the user finishes typing a word. Takes list of words `sofar`, list of words `prompt`, user's `user_id`, and an `upload` function to upload progress. The progress will be a ratio of correctly typed words in prompt until the first incorrect word divided by the len(prompt).
- a `time_per_word` function taking a list `words` and `times_per_player`, a list of lists for each player timestamps when finished typing each word in words. Returns a `match`, which is a dictionary storing words and times by iterating through each players times.
- a `fastest_words` function that returns the words each player typed fastest. This function is called when both players are finished typing after a `match`. Therefore, it returns a list of lists of words per player where each player has the fastest words they typed.


