### Unforgettable UX: Designing for a Poor Memory by David Swallow

* Recall vs. recognition.
  * A recall test: Who wrote Moby Dick?
  * A recognition test: Did Herman Melville write Moby Dick?
  * Recognition is generally easier, which is why multiple choice questions are easier
  * This distinction is helpful for UX design
* Memory loss can be caused by so many causes
* Recognition over recall is [one of Jakob Neilsen's heuristics](https://www.nngroup.com/articles/ten-usability-heuristics/)
* [Miller's magic number 7 (+/- 2)](https://en.wikipedia.org/wiki/The_Magical_Number_Seven,_Plus_or_Minus_Two) is commonly discussed as the number of items you can keep in working memory, but not that helpful in practice.
* WCAG 2.1 and 2.2 started adding some memory-based success criteria, pushed by the Cognitive and Learning Disabilities Accessibility Task Force (COGA)
* [Making content usable for people with cognitive and learning disabilities](https://www.w3.org/TR/coga-usable/)
* There is so much more to it than passwords
* But passwords are a good place to start, since they are problematic for everyone, especially anyone with memory loss
  * Then people adopt workarounds that make it less secure
  * "Everyting wants a password now"
  * Important to make sure our apps don't make it unneccessarily difficult to use a password manager
  * Allowing paste a confirmation code from text is useful, they mean that you don't have to context switch
  * [W3C WebAuthentication API](https://www.w3.org/TR/webauthn-2/)
* Search
  * Making things searchable is useful: once you type in your query, finding the result that you forgot about is just a recognition test, rather than a recall one
  * Autocomplete helps with recognition when putting together a query
  * Did you mean, search suggestions, filters are helpful
  * Consider the presentation of search results, not too busy or overwhelming
  * Google is often more forgiving than site searches (Did you mean?)
  * ...but it doesn't help if all the information is in infographics and videos rather than searchable text
  * Searching browing history: having unique page `<title>`s are very helpful for this, rather than using the same title for each page
    * Also, there are challenges with single page apps
* Navigation
  * remembering where you are going, how to get there, where you have been, etc.
  * Unclear page structure and Taxonomies that are unforgiving are challenging
  * Multi-page forms are a challenge
    * For example, checking out on an online shopping site and it does not include a summary of the transaction in practice on each page of the form
    * Repeat instructions on each page, don't rely on people remembering things from page by page
* Forms
  * Text labels, *not* placeholders
  * Icons can be good once people understand what they mean, but no icon is universally recognizable.  If you include a text and an icon, then you introduce it well and then they recognize the icon on subsequent visits.
* Using browser tabs as a to-do list, freeing up working memory.  The tabs become almost breadcrumb navigation, with like 200 tabs open at a time.  It's awesome that browser can handle hundreds of tabs and remain performant now!
* Much of this advice is standard accessibility good practices -- not new things to do, but further reasons to do the same things
* Distractions
  * Modals and gdpr consent are so distracting: "by the time I have turned off cookies on a site, I forgot why I am at that site in the first place"
  * Auto-playing media is distracting
  * Low contrast text is harmful
  * Reading mode in the browser can be a workaround that users employ


### Web Accessibility for Speech Recognition Users by Shashank Kapur

* Shashank is from BarrierBreak.
   * Nearly half of the testing team members at BarrierBreak are people with disabilities, and people with disabilities are part of all testing projects
* Speech recognition helps with mobility disabilities, temporary and situational disabilities, and multi-tasking
* Speech recognition tools:
  * Dragon Naturally Speaking and Speech Recognition on Windows
  * Voice Control on macOS/iOS
  * Voice Access on Android
* Smart assistants cannot fill in a form, navigate a web page, write a word document.  So this talk focuses on speech recognition
* Interaction methods:
  * "Click Submit"
  * "Show numbers" -> see which number is the interactive element you want -> "Click five"
  * "Show labels" or "Show names", if visual label is missing or if you need to select an image from a page and you need to know what its name is
  * Mouse grid: requires a series of commands, time-consuming.  Handy when websites aren't built well.
  * Dictation command.  You can even tell it to add a heading or list.
* Things that cause issues
  * It causes an issue if multiple elements have the same label, because if you say "Click [x]", it won't know what to do.  Links with identical text, for example "Learn more..."
  * No keyboard focus indicator
  * Image alt text doesn't match the image.  Or missing alt text
  * content only available only on mouse hover, dropdown menus, or tooltips, since it can require mouse grid
  * clickable area too small -- even mouse grid can't be effective here
  * Accessible name does not match visual label
  * Looks like a button but is actually a link
  * drag and drop without an alternative way to interact with it
  * content not visible
  * modals
  * focus not managed correctly
  * inconsistent naming (e.g. it is called "Search" in one place, "Find" in another)
* Techniques
  * unique and descriptive text labels for all ui controls
  * nice focus indicator
  * native HTML semantics, rather than custom
  * include visual label at the start of accessible name of controls
  * label the form inputs
  * avoid unpronouncable labels (acronyms, abbreviations, etc.)
  * avoid extra spacing between words, makes it harder to recognize it as a phrase
  * limit iframes
* How to start
  * They test using Dragon + Chrome, then iOS + Voice Control and Android + Voice Access
* Multilingual environments: very important to use the `lang` attribute
* Different issues can come up with screen reader testing vs. voice control (or both at the same time).  Important to do both.
* To learn how to test with it, just start using it all the time, incorporate it into your daily work.  Doesn't have to be dragon, just give the built-in option a try.  Youtube it, get used to the different modes (normal commands vs. numbers vs. mouse grid), so that when you run into an issue, you can know if it's an issue with the page or you just don't know the right way to interact with it.

### The First WCAG AAA Compliant Digital Campus Map by Brandon Biggs

* 
