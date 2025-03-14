### Digital Accessibility Legal Update: US

Presented by Lainey Feingold

Digital accessibility: the difference between inclusion and exclusion for disabled people 
Accessibility is security and privacy -- if it is not accessible, disabled users do not have security or privacy 

A quarter of accessibility lawsuits last year were against organizations that use an overlay

Lainey highlighted [an article on her blog about recent OPM memos and DOE civil rights investigations](https://www.lflegal.com/2025/02/singling-out-disability/) -- in both cases, DEI + A were targeted initially, and then the federal government retreated to targeting DEI.  Neither reversal is a cause for celebration, more of a divide-and-conquer strategy.

#### Staying informed and keeping hope

[Civil rights Clearinghouse](https://clearinghouse.net/): good place to see what lawsuits are pushing back on behalf of civil rights, she recommended this as a source of hope! 

Two good resources to stay current:
* [Dredf](https://dredf.org/)
* [Seyfarth Shaw Title III blog](https://www.adatitleiii.com/)

### Design Systems: An Accessibility Team's Best Friend

Presented by Daniel Henderson-Ede from Mantis & Co

Pressures on design system teams (similar goals and pressures)
* Design systems are responsible for holding up many responsibilities within the organizations (conversations about "have design systems oversold themselves?").
* Many articles lately about design system metrics
* Design systems try to scale design tokens, brand guidelines, content guidelines, design consistency, team efficiency, engineering practices

A design system has no intrinsic value -- it has to be used!

How are design systems measured?
* Adoption -- how many pages use it?  proportion of components on the page that are from the design system?
* Product consistency?
* Speed of development
* Office hours attendees

89% of design systems include documentation about accessibility.  Some of this documentation is more effective than others, though!
* Recommendation: don't put this into a separate Accessibility tab, good accessibility guidelines should be woven throughout the guidance about how you use it

There was an interesting quote, I did not catch who said it originally: If you work full-time on a design system team, you do not "own" the design system, you are a full-time design system practitioner.  The organization owns the design system, and everybody should be contributing to it.

Idea: give the accessibility of each component a letter grade.
Counterpoint: Design systems should represent the very best engineering practices of your organization, if it is not accessible, it is not the best, so it should not be in the design system to begin with.

### Designing Keyboard Behavior for Diverse User Types

Presented by three people from Oracle (I did not catch all of their names)

[Keyboard behavior slides](http://a11y.work/keys.pptx)

#### Context

Web applications are becoming increasingly complex.  Many blind users and users with motor disabilities rely on keyboard navigation.

#### Audiences

Two audiences: sighted keyboard users and screen reader users.  Screen reader users use all the keyboard navigation that sighted keyboard users do, and more "because we're cool!":
  * arrow keys
  * screen reader hotkeys

So keyboard interaction may be really great already thanks to a screen reader, but not for sighted users

#### Designing keyboard experiences

When designing keyboard experience for a widget:
* Follow established HTML pattern if possible
* If not, follow established Aria pattern if possible
* If not, do comparitive research to find established patterns

Definitely think about how often users will be new to the page, how much will they be using it (i.e. using it all day as their job)

Don't try to be fancy.  Try to be simple!  For example: the dropdown to choose the state/province of your address.  Just use the typical HTML that allows you to type the first few letters, rather than something fancy/custom that is frustrating to navigate.

For power users: keyboard shortcuts
* Don't conflict with hotkeys for screen reader, OS, or browser
* At the same time, try not to have things that require a ton of keys to be pressed at once (e.g. Shift+Alt+Windows Key+three other keys)

UX research is key -- important not to rely on one person's experience (a screen reader power user of the application wouldn't be representative of a screen reader user new to the software)

As an illustration of the above, we spent much of the session trying to determine the appropriate keyboard interaction for a common UI element: a typeahead chip situation, in which you can remove existing chips.  Should each chip be a tab stop or an arrow key stop?  Separate stop for the close action?  What about the aria grid pattern from the Aria Authoring Practices guide?  Different answers depending on how experienced the user is?  Everyone in the room had a (different) opinion, it was pretty funny!

### Creating a Hyper-Accessible Website for VI and Sighted Visitors

Presented by Sandy Shin (Braille Institute of America) and Jeremy Perkins (iFactory)

This presentation was about a redesign of the [Braille Institute's web site](https://www.brailleinstitute.org/)

Two main audiences for the site: blind and low vision.  Low vision users are a growing segment.

#### Major UX choices

* Personalizing (low vision can be very different, depending on the diagnosis)
    * Huge button in the top of the page with three checkboxes (large text, light mode, and dark mode)
    * simple onboarding to make the website customized to what you need
    * Goal to have very few options so there is not much cognitive load for screen magnification, or for somebody recently diagnosed who is not familiar with all these accessibility settings, or who is low vision and doesn't know if the site is for them
* Enlarge all text except H1 and H2
* separating content with black lines, not just whitespace, was helpful
* optimize for screen magnification -- make sure that everything useful is in the "F" pattern
    * There is very little text copy
    * Cool marketing images are present, but they are on the right where it is less in the way

#### Design process

* Figma prototyping was not an option.  They did an html prototype
* Tested with 5 low vision users (both with and without accessible technologies), 5 blind, 5 sighted
* In testing, they learned:
    * They had eyebrow text before headings.  Without the styles, the eyebrow text was under the previous (unrelated) heading
    * toggle button placement, change so that the toggle comes first for screen magnification
    * icon fonts were problematic: it would cause a pause in JAWS.  Better to remove the icons.
    * Make the text copy more specific
    * Change filter behavior (not radio buttons) -- [this reminded me of the allsearch jump to section](https://www.brailleinstitute.org/find-services/offerings/)

#### Guidance

* Talk to users and understand how they think about themselves
* Consider the experience across pages
* Consider every design and content detail
* Be prepared to change course when testing
* Beware of common ui patterns (icons, centered or right-justified text with lots of white space)

### Blind Innovators for the Blind: The Bill Gerrey Model

Presented by James Coughlan (Smith-Kettlewell Eye Research Institute), Sile O'Modhrain (University of Michigan), Joshua Miele (Amazon Lab126), and John Brabyn (Smith-Kettlewell Eye Research Institute)

This was a very nice overview and rememberance to [Bill Gerrey](https://www.ski.org/news/skeri-mourns-passing-bill-gerrey), an electrical engineer, scientist, inventor, blind advocate, and mentor.

* Invented numerous innovative tools for blind individuals in a vaiety of settings, especially in specialized fields:
    * HAM radio
    * Micrometers
    * Multimeters
    * Carpenter's levels
    * Oscilloscopes
    * CNC milling machines
    * commercial freezer gauges
    * soldering for hobbyists and professionals -- a course
* Shared and propagating his inventions and methods, before "open source" was ever a thing, through the [Smith Kettlewell Technical File](https://www.ski.org/smith-kettlewell-technical-file)

> When you design something for yourself, it's not enough to meet just your needs.  You owe it to the rest of the world to make sure that it works for everyone.

It's important not to just have blind people as study participants, but also driving the research as principal investigators.


### Informal conversations

Somebody mentioned Amazon Textract as an OCR tool that keeps all of the structure (e.g. tables) from the original document, can OCR a scanned table into a database
