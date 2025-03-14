### A Tale of Two Washingtons: Partnering for Accessibility

Presented by Betsy Sirk (NASA), Mary Craig (Washington State Department of Services for the Blind), Owen Chong (NASA)

Betsy chairs an accessibility industry outreach program
* Helping industry understand accessibility, section 508, VPAT/ACR, and other topics, and collaborating
* Section 508 of the rehabilitation act: it is specific to federal agencies, but has a big influence on other governments and on industry.  And there is lots of confusion and misinformation about it.  Hence the need for outreach to industry on the topic.

Internally at NASA, NASA developers have to do a VPAT/ACR for their software before implementing it, just as if they were a commercial off-the-shelf product

Accessibility Matters conference in Washington State

### The New Touchscreen Experience for Audiom Web Maps Is Here

Presented by Brandon Biggs (XR Navigation)

[Audiom - accessible web maps](https://www.audiom.net/)

#### Constraints to use audiom with a touchscreen

* This is a web component, where we can't use custom gesture inputs with screen reader running
    * VoiceOver and Talkback take over all the gestures except for one-finger tap and one-finger double tap
    * The only option for implementing custom gestures would be "direct touch" -- this is an option for native apps but not for in-browser situations
* Needs to handle all 3000+ features on the map and still be performant
* Needs to work with a mobile screen reader and desktop screen reader
* Needs to be intuitive to new users

#### Existing solutions
* Vibro Auditory Maps (integrated into Apple Maps)
    * hard to make this intuitive in a web page, especially since screen reader captures all the gestures and does not pass them to the browser
* Games

#### Approach they took
* Use a Button panel: this way you can swipe between the buttons and tap the direction you want
* Use a button to open a menu as well
* Also the option to type in MUD game-style commands using built-in keyboard, bluetooth keyboard, or [braille input in voiceover](https://support.apple.com/guide/iphone/type-braille-on-the-screen-iph10366cc30/ios)

#### Future needs
* Apple and Google should allow direct touch in the browser
* Vibrations and haptic is cool, but no studies show that they are super effective.  How much value would it add to the experience?
* Next step is voice gestures/commands (users said touchscreen was the most important, then voice)

### Accessible Cybersecurity

Presented by Pam Mayer and Divya Nagaraja (Workday)

[Accessible cybersecurity slides](https://workday.app.box.com/s/gg2f75pvzvakgoeosh6bee85qpsukk6h)

* [Flubot - a malware that used accessibility features as part of the attack](https://www.withsecure.com/en/expertise/blog-posts/flubot_doh_tunneling), there are a few other malwares recently that also used these features

### Digital Accessibility Legal Update: Beyond the U.S. and EU

Presented by Lainey Feingold and Shilpi Kapoor (BarrierBreak)

Many countries (Kenya, Australia, Mexico) are adopting EN 301 549.

### Embedding Accessibility into a Design System Playbook

Presented by: James Carleton, Aidan Tierney, Cordelia McGee-Tubb, all from eBay

They presented on [their design system](https://playbook.ebay.com/design-system), which seems to be called both "Playbook" and "Evo".

One interesting thing they mentioned was about providing guidance around "prefers reduced motion".  For my taste, even their reduced motion version had a bewildering amount of motion in it.  [One of the foundations of their design system is motion](https://playbook.ebay.com/foundations/motion).

### Creating Accessible Design Systems

Marcelo Paiva, Sarah Massengale, Claudio Luis Vera

This session was so cool!  They asked for volunteers to show a component in their design system, and they tested the component LIVE for you, and provided feedback along with the audience.  They were kind enough to take a look at the [Lux Disclosure component](https://pulibrary.github.io/lux-design-system/#!/Components/LuxDisclosure).

They also had a great metaphor:

> An accessible design system is like Home Depot: you can buy an accessible door at Home Depot, but if you install the door into a building without a ramp, it won't be accessible.

More plainly: even if a component in a design system is very accessible, you can still use it in a page in inaccessible ways
