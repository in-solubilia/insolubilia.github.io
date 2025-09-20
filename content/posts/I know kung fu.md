---
title: I know kung fu
description: " An RSVP reader with extra features such as capturing highlights and taking notes."
date: 2025-09-20T12:55:26+00:00
draft: false
---
<a href="../I-K-K-F-!.html">IKKF</a>: An RSVP reader with extra features such as capturing highlights and taking notes. This tool is meant to be usable both online and offline. CSS/HTML/Javascript are all on the page-- if you want, you can save it and use it on your own.

RSVP, or rapid serial visual presentation, is a method of speedreading where the words are displayed on the screen one at a time for a set amount of milliseconds. I like it. I think it's good for getting through the news, with larger "chunks" (more than one word at a time) preferable for denser prose. I wouldn't recommend it, of course, if you're looking forward to luxuriating in Literature, but it is good for just getting the reading done.

I like taking notes as I read, and in most RSVP programs I've tried, if I wanted to directly quote the text, then I would have to go search for the string in the source and copy it out. So, I made this tool to add more notetaking/highlighting functionalities on top of the existing RSVP method.

I am a big amateur so the code in this is probably not as clean as it could be. A lot of it is very miscellaneous copypaste, but if any functions are directly lifted from somewhere, I have a comment with the source.

Other cool RSVP projects: [Hot Gato](https://hotgato.com/), [Stutter Firefox addon](https://addons.mozilla.org/en-US/firefox/addon/stutter/reviews/?utm_source=firefox-browser&utm_medium=firefox-browser&utm_content=addons-manager-reviews-link)

I K K F = I Know Kung Fu... :)

8/21/25:

- Added edit option to manually taken notes
- Swapped out the slider bar for an entry field
- Swapped out the keyboard shortcuts popup for a hover tooltip and then swapped that for just text... still not sure how I want it to look
- Fixed some weird flex stuff when panes get toggled

8/12/25:

- Cleaned up some CSS funkiness
- Added new controls for highlights to expand back and forth by word or sentence after capture

8/3/25:

- Added the option to toggle between 1, 2, or 3 words shown at a time
- Added some hover tooltips

7/24/2025:

- Highlighting will capture displayed span of text and save to Notes section, function is toggled on and off with H key
- Highlights will expand to capture start and end of sentence if the highlight lasts for longer than one sentence (Trying to anticipate any Bolanoesque edge cases)
- Notes can be manually added with an entry field
- Notes are saved as markdown files for ease of integrating into [Obsidian](https://obsidian.md/)
- Saved notes are automatically named after the uploaded file
- Reading material can be added by uploading a text file or by pasting text into an entry field
- Punctuation and words over 10 characters get a slightly longer pause by default
- Keyboard shortcut support
- Reading pane, options pane, and notes pane can be toggled on/off for better visibility
- Font, background color, and overall color scheme are all customizable
- Added font selection

- Add save support for other filetypes
- Add ability to take .html files, such as the ones captured by [Shiori](https://github.com/go-shiori/shiori)
- Add ability to take epub files
- Add support for displaying and pausing on images
- Add user input for enabling/disabling/adjusting the extra punctuation and long word pauses
- The time estimate is for sure busted, need to fix
- Add easily accessible download link for offline use
- Add option to have a longer pause for numbers/statistics
- Add option to have "focus" letter in center of word chunk
- Add full hover tooltips
- Add post-creation edit to manual notes
- Add reverse/undo functionality to the note expansion buttons
- Add mobile support?
- Fix remaining CSS funkiness...