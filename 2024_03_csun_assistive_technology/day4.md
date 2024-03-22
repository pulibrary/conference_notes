### Testing WCAG 2.1.1 Keyboard on Mobile by Moaan Ahmed, Sam Ogami, and Purva Sane

* [slides for keyboard on mobile testing](https://bit.ly/wd-aks)
* They do monthly accessibility office hours
* They wanted to understand WCAG 2.1.1 keyboard on mobile better.  Wanted to know more about keyboard users on mobile, and how to test efficiently?

#### Keyboard on mobile users

* they focused on users with motor disabilities, but also users with visual disabilities and reduced dexterity
* they looked at input options in android and ios:
  * switch control (ios) / switch access (android)
  * voice control (ios) / voice access (android)
  * assistive touch (ios) / timing controls (android)
  * external keyboard -- the experience depends a lot on the OS and OS version
* they wanted to learn more about the experiences users had, so they did a survey
* a major pain point: lack of documentation about keyboard shortcuts
* when keyboard support is lacking, users had to fall back on screen readers, voice control, and other assistive technologies

#### testing keyboard access

* The on-screen keyboard definitely doesn't work, it doesn't have any modifier keys for keyboard shortcuts!
* If a site or app works well with VoiceOver and TalkBack, it does not guarantee that it will work with keyboard access -- very different from desktop testing experience
* If you are testing for keyboard access, you also need to check 2.4.3 (focus order) and 2.4.7 (visible focus)
* You should test with keyboard + screen reader, and also test with keyboard only -- the experience is quite different
  * Android doesn't even document what the Talkback keyboard keystrokes are!

#### testing procedure

* connect mobile device to bluetooth keyboard.  If you are testing on multiple mobile devices, get a keyboard that can connect to multiple, and switch back and forth
* On Android, you just connect the keyboard and you're good.  On iOS, you have to change a setting to enable keyboard access
* The Android/iOS simulators and emulators don't work for this testing -- especially the Android one.
* Android: many keyboard shortcuts rely on the "search icon" key -- typically the meta key or command key
* Android: shortcut list is search icon key + /
  * this includes both the system shortcuts and app-specific shortcuts
  * ios: tab + h
* Android has this horrible panes notion, you get trapped in them, and you have to Search + Tab to switch between them.  It is not documented, doesn't even work on all bluetooth keyboards, and causes a lot of problems
* It's okay if actions aren't focusable, as long as you can reach it through a keyboard shortcut that it documented in the shortcut list
* [Their testing procedure](https://bit.ly/wd-aka)

### The Crossroads of Accessibility and Localization by Erin Lucas and Katherine Zinger

### CSS + Accessibility: Inclusion Through User Choice by Carie Fisher

### Using the Accessibility Tree to Debug HTML by Christina Adams
