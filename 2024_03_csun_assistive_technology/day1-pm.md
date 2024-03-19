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
