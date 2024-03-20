### Accessible Terminal Application for Screen Reader Users by Takahiro Miura and Junji Onishi 

* [research paper related to this presentation](https://csun.at/draftvol12) (pages 185-197)
* Background
  * IDEs are becoming increasingly complex, presenting additional accessibility challenges
  * [Grid-coding style is one approach](https://pure.psu.edu/en/publications/grid-coding-an-accessible-efficient-and-structured-coding-paradig)
* WEBBY Term is their terminal
  * It keeps the last output of STDOUT saved temporarily so that users can easily review in a complementary window
  * Notification with sound effect when the execution of the command completes, so that you know it's time to review the output
  * screen scrolling functionality
* They tested with blind and low vision computer science students
  * most used NVDA, 2 used PC-Talker (Japanese screen reader), 1 used JAWS
  * the test included switching between the terminal task and other web browser tasks (e.g. start `git clone` in the terminal, go search something unrelated, and go back to `ls` the cloned repository when it was done)
  * Tasks were done on both PowerShell in WEBBY Term
* Feedback:
  * Powershell presents challenges in navigation, checking details without redirecting STDOUT somewhere else
  * WEBBY Term uses standard keystrokes
 
### Latest Survey Findings from Online Disability Communities by Norbert Rum, Nick Goodrum, and Charlie Beach

* [Slides of the survey presentation -- powerpoint](https://bit.ly/WebSurvey2024)
* [Findings are available here](https://webaccessibilitysurvey.com/)
* The [r/blind subreddit](https://www.reddit.com/r/Blind/) was created in 2010, where this survey began
* Noticed that there were some discrepancies between what surveys said, and what their experience was
* They went to other online communities, not just r/blind.  They reached out to WebAIM too.  And they made it really general, not just about screen reader users, but all users of assistive technology
* It was structured to allow you to select which technologies you use (e.g. somebody could say that they use a screen reader, a screen magnifier, and other technologies)
* The reddit blackout happened during the survey, which influenced results (there are some negative comments about reddit, for example)
  * r/blind was a key part of this discussion in the news media, showing that accessibility was a big deal
* 45% of participants use screen magnification -- we should pay more attention to magnification in our work!
* Unlike the WebAIM survey, NVDA is the clear leader as primary screen reader
* The majority of respondents only used a single screen reader
* CAPTCHAs -- not a good experience.  11% fail CAPTCHAs every day.  Half fail every week or more frequently.
* Overlays were *not* generally appreciated
  * Pros
    * option to remove animations
    * fixing divs with onclick handler
  * Cons
    * they steal focus
    * they are memory hogs that crash the browser
    * they start the screen reader reading twice at the same time
    * they make the site inaccessible
    * some people didn't run into issues because they block overlays, or just don't use sites with overlays
* Lots of users use mobile devices with keyboards.  And keyboard navigation is not intuitive on mobile.
* Screen reader users
  * 66% of the time, navigate by headings, landmarks was only 15%
  * 44% of screen reader users use a mouse at least sometimes (e.g. screen magnification to a very high percentage, then use screen reader for words that are too long to fit on the screen)
  * Screen readers are used by more than just blind and low vision people
* only 18% of screen reader respondents used a braille reader
* Survey fatigue: r/blind gets constant survey requests from universities
* The survey software was selected because it was the most accessible, but there were still a few issues (e.g. it was difficult to use with high amounts of screen magnification)

### Designing Your Own Accessibility Vendor Monitoring Program by Juanita George

* [powerpoint slides for the vendor monitoring presentation](https://drive.google.com/file/d/1UxWupjK169YFiXgtkL6_sEkSV6SUqHqw/view)
* Importance of a vendor program
  * Customers can't tell where your product ends and when the vendor product begins
  * You can't have a diverse workforce if you don't purchase accessible tools
  * Vendor claims need to be validated
* Build relationships with procurement people
* get access to the database of contracts, and start documenting
  * last accessibility audit date and results
  * bugs and fixes
  * ACRs
  * their public accessibility policy, etc.
* other teams may be inventorying vendors for other reasons, build relationships with those people
* what makes an ACR more reliable?
  * Assessment done by a qualified, reputable independent third party
  * Tester name provided
  * Testing tools and processes included
  * Detailed information provided
  * Date is recent
  * Based on a full audit of the product
* To validate vendor claims, do some smoke testing -- timeboxed quick checks, including users with disabilities.  Let the vendor know you are doing it.
* Think about the vendor's own accessibility team: can you do things to help the vendor's team?  Deliver smoke testing results in helpful ways, make it clear how important accessibility is to us.
* Create a monitoring plan, expect and plan for non-conformance
  * Figure out how you can do this without taking up all your time -- timeboxing
* Know when vendor renewals are taking place and be involved in the conversation

### Accessibility QA for eBooks: Are Automatic Tools Enough? by Gregorio Pellegrino

* 
