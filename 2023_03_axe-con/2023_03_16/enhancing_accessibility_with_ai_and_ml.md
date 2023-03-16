# Enhancing Accessibility with AI and ML

presented by Noé Barrell
Slides: https://www.deque.com/axe-con/wp-content/uploads/2023/01/Axe-Con.pdf

https://docs.google.com/document/d/1xPNB14V7SNcxsMRGJadCCSNsFx22supppSCgjTNJDr4/edit

ChatGPT creates inaccessible code samples, since it is trained on inaccessible code

Deque is using OCR and computer vision to identify parts of a website.  Some examples of what it can identify:

* A form where labels are not programmatically associated with their inputs -- it can identify the labels based on the layout of the page
* A site uses a div when it should be a checkbox
* A tab for navigation: it has "button" role, but should have "tab" role
* Complex table that is missing headers

Their algorithm considers the relationships between screens (e.g. tab navigation: on one screen, the tab is selected; on the others, the tab is not)

When axe-pro detects an issue, it informs the user and asks if it was correct.  If it was wrong, that is added to the data set.

Axe-for-designers: a figma plugin that uses their machine learning model.  Currently free beta.

## Unique machine learning challenges in UI interpretation

* UIs can be very dense -- lots of objects on top of each other or near each other
* Widely varying sizes (an icon is small, a footer might be quite large)
* Training data needs to be collected with accessibility in mind (very few accessible examples) and needs to be labeled by UI experts
  * One screen can take 30 minutes for one expert to label!
