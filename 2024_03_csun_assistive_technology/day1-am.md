### Keynote: Disabled People Drive Innovation by Haben Girma

* [Recording on youtube, talk starts at 35:32](https://www.youtube.com/live/WW7erYVOej4?si=h5781GMrdL0B9mJD)
* Very great keynote!
* Opening up communication to include more people can take some time, and it can be unexpected, but ultimately it makes it better for everyone
* She shared a story of going to a bar with a keyboard braille display -- it ended up that her classmates really appreciated communicating via keyboard and braille display, because they don't have to shout over the loud music
* Designing for the Deaf community, or for disabled communities can end up helping lots of other people too (email, gestural touch based interaction)
* Connection between assistive technology and right-to-repair legislation: when people finally find some technology that works for them and their body, and it breaks, it is hard to get it repaired, and the new version might not work as well for them
* "My disability did not prevent me from doing the jobs, it was Ableism and employment discrimination"
* Disabilities are opportunities for innovation
* "Sometimes when people are working on tech, there is a desire to simplify the disability community.  TO flatten us to one dimensnion.  THere is a desire to downplay the different sign languages around the world"
* [Protactile](https://en.wikipedia.org/wiki/Protactile): a language centering touch-base communication
* Example of Lewis and Clark College: they said "we haven't worked with braille displays before, but we're willing to put in the work" -- except the dining hall
* There is the idea that non-disabled people are independent.  That is not true.  "Many of you like drinking coffee, but few of you grow your own coffee beans."
* The difference between accommodations for sighted people and for blind people is Ableism.  Lights, slides, microphones, chairs -- these are all accommodations for sighted people, hearing people, walking people that cost money, just as accommodations for disabled people do!
* There are many barriers we dismiss as small, we think "is it really that big of a deal?, there are worse things in the world".  But advocating for the small things is how we learn to advocate for the big things.
* Add descriptive transcripts to videos!
* [We have her book in the collection](https://catalog.princeton.edu/catalog/99115204113506421)

### Beyond Checklists: Inclusive Co-Creation with Disabilities by Manish Agrawal

* Manish Agrawal is the founder of [IAccessible](https://www.iaccessible.net/about-us), used to be product manager for Microsoft Narrator
* Disabilities are created by designers
  * Example: a call center form has a country field that is technically accessibly, but you have to press the down arrow several hundred times in order to reach "United States".  The form passes the checklist, but it could prevent somebody with a motor disability from working in that job.
* Myth: usability is a touchy-feely thing that can't be measured.  It can be measurably improved:
  * Efficiency
  * Error rate
  * User satisfaction
  * Learnability
  * Memorability
* This all adds up to be the "disability cost".  And the disability cost keeps going up -- paying a bit more time and effort to do the same task.
* Even if a team creates a usable inclusive product, the next update could ruin it
* Including people with disabilities is the obvious part of the solution.  It is hard to guess the right solution without lived experience of disability
* Get inputs from a broad spectrum of disabilities -- being blind does not make somebody an expert in, say, cognitive accessibilities.  But some progress, and getting some feedback is better than none.
* Case study: Adobe working with iAccessible
  * Adobe wanted to design *with* users with disabilities, not *for*.  Wanted to educate engineering teams.  And wanted to make sure their WYSIWYG editor was accessible
  * Adobe and iAccessible did a very iterative approach by sending prototypes back and forth
  * Engineers saw the actual user impact each step of the way, rather than just a list of bugs -- transformed the engineering team
* Compliance (e.g. WCAG) is a baseline, not an end goal
* When teams try to be inclusive, but don't actually include people with diabilities in the process, it leads to "disability dongles"
  * e.g. a big long aria label that says "please click the big green button in the middle of the screen" -- not helpful!
* Strategies:
  * Hire people with disabilities
    * Working with a peer, and seeing them experience problems in the system, is so critical -- it's no longer a "far away" issue
    * Build hiring systems to be inclusive
    * Build inclusive enterprise environments and accommodations programs
    * Build ERGs and support groups
  * Include people with disabilities in all user research
    * train researchers on including people with disabilities
    * recruit from ERGs
    * Work with outside companies to get help with creating inclusive research studies (and they will probably recommend that you include people with disabilities in all usability research)
  * Get people with disabilities to design and assess your products
    * Much better able to articulate the best fix, and prioritize according to impact
  * Make it easy for assistive technology users to provide feedback
    * Most organizations make it very hard to report issues.  This means that you are missing out on free usability testing!
    * Train customer care teams about accessibility and assistive tools (they can try to be helpful, but if they have no idea what a screen reader is, how can they understand the issue or escalate it to developers?)
    * Example of the Disability Answer Desk at Microsoft -- highly trained, have the access to the engineering teams to get things fixed
  * Simulations as a double-edged sword.  The feedback you get from a blind user vs. a sighted user wearing a blindfold will be quite different.
  * How can you get feedback before you have working code?  E.g. if all you have are wireframes, how can you get feedback from blind users
    * Definitely people with low vision doing design reviews
    * Have the product/engineering teams describe the screens to blind people, answer questions like "what will the screen reader say when it lands here?", "what is the focus order?" -- visualizing it as a screen reader might.
    * [Wizard of Oz methodology](https://www.nngroup.com/articles/wizard-of-oz/) was a suggestion, where one person takes the role of screen reader
  * Points from the audience about the value of contracting out for this work:
    * one form of resistance is just that the engineering teams have a million other things on their plates.  So contracting it out can free up engineering team.
    * engineers are not a representative sample of users!
    * contractors can be trained to use very niche software (e.g. a security software that requires background knowledge)
  * Example from testing at Microsoft: the blind users said "I have no idea when copilot is available is not."  And it turns out that this was a usability issue affecting everyone, Microsoft just hadn't picked up on it yet.
 
### Single Page Application Accessibility by Doug Abrams

* Doug Abrams is a Senior Accessibility Engineer at The Paciello Group
* [Powerpoint slides for this talk](https://visperoinc.sharepoint.com/:p:/s/TPGiPermalinks/EYgFJ8gxbLxNqil8KLYYgIUBXq_KUZ2Z0KR9LIPHR_J44w?e=a8rSx2&download=1)
* Two types of challenges:
  * Direct challenges are a result of how the framework behaves
  * Indirect challenges are when the framework makes things harder for the developer to find and fix the issues
* Direct challenge in dynamic content: managing focus
  * Manage content when it is added (if items are dynamically added to a list, set focus to the first new list item)
  * Manage content when it is lost (if you delete an item from a list, what happens to the focus that was on the delete button?)
  * We don't want focus to move back to the `<body>` or end of the page
  * Focus also affects magnification software
  * [Helpful article](https://www.tpgi.com/how-to-avoid-breaking-web-pages-for-keyboard-users/)
  * How to fix:
    * Identify where focus should go
    * Make sure it can get focus (`tabindex=-1` if needed)
    * set the focus.  But some frameworks make this difficult, since they don't want you specifically working with the DOM with methods like `document.getElementById()`
* Direct challenge: page navigation
  * Very helpful resource: [Marcy Sutton's research on the best way to announce client-side routing](https://www.gatsbyjs.com/blog/2019-07-11-user-testing-accessible-client-routing/)
  * Update the page title
    * especially important if they move to another tab, and have to move back to the tab
  * Set focus to the first heading of new content
  * Make sure the focus indicator is visible
* Indirect challenge: HTML is simplified into components (which may not even use html)
  * Developers lose insights into the semantics of what they are writing
  * Using divs with onclick events, for example.
  * This is an indirect challenge: developers are looking at components, while testers and end users interact with the rendered HTML -- they are not even working with the same things (developer sees `<my-great-button-component>`, end user sees `<button><img src="i-have-no-alt"></button>`.
  * It's important for developers to learn more about how components render with various props, especially for any third-party components
* Indirect challenge: reusing components in different contexts
  * If a component contains a heading, reusing in a different context could give an illogical heading structure
  * Image alt text may change according to context and what you are trying to convey in that specific page
  * The meaning of a link may also change according to context
* Indirect challenge: third-party components
  * It's very easy to grab a new 3rd party component from npm, push it out to users, without ever even seeing what HTML is rendered, much less looking into accessibility
  * The component might say "it is accessibile out of the box", but you should always dig deeper.  It can sometimes be a way for them to absolve themselves of accessibility responsibility ("our component is great, if there's an accessibility issue, it must be in your app").
  * Read the accessibility documentation!  If there isn't any, or if it's minimal... that's not a good sign.
  * Test your site, including people with accessibilities in the testing ("nothing for us without us")
* [Gatsby is a React-based framework with a good focus on accessibility](https://www.gatsbyjs.com/)
