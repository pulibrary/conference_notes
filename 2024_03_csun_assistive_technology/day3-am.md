### What's New in Google Accessibility by Perrin Anto, Jonathan Bernal, and Cynthia Shelly

* [Youtube video recording of what's new in google accessibility](https://www.youtube.com/watch?v=p34rx5tk8Tg)

#### Android

* Lookout: you can have an interactive Q&A about what is in an image.  For example: if you give it a picture of a dog, you can ask if the dog looks playful
* Talkback: new assignable commands for physical keyboard if you use a keyboard with your android device
* [Non-linear font scaling](https://developer.android.com/about/versions/14/features#non-linear-font-scaling): the small text gets bigger by 200%, the big headers get only slightly bigger, so that you don't have to scroll and scroll past humungous letters
* Notifications via camera flash -- this was a feature that people advocated for at accessibility conferences, which helped the accessibility teams to prioritize it
* Live captions and live transcribe: they have added language
* Project Euphonia - project to include people with non-standard speech in their training sets.  It led to Project Relate, a feature where you can train your own phone to recognize your voice and speech patterns by saying five things.

#### Chrome

* Reading mode now generally available
* Read aloud coming to ChromeOS in the next few months, so that it can read to you as you read
* they are improving the chromevox voices
* They have a new feature: if somebody is using ChromeVox on their chromebook and they come across an inaccessible PDF, it will automatically OCR it

#### Workspace

* Google slides now lets you present slides with captions
* Google docs has a feature where you can type with your voice
* [Article about making fonts more accessible](https://material.io/blog/how-to-make-text-more-accessible)

#### Maps

* You can search for walking and public transit routes that do not have steps to climb up/down

### Automating Accessibility: Tying A11Y to Your Build Pipeline by David Martin, Kenneth Bigler, and Sabu Philip

* The presenters are from Intuit
* Two of the three presenters work in security positions, rather than accessibility positions
  * There are connections between security and accessibility in businesses: both can be seen as "extra" things that developers/companies don't want to invest in.
  * However, they find that it is easier to talk to upper management about security than accessibility in terms of money and risk
  * Intuit has 300 full-time security people, only 3 full-time accessibility people
  * They find it helpful to talk about accessibility to executives in terms of reputational risk.  They don't want a negative newspaper headline.  It helped that one of Intuit's recent acquisition was sued for an inaccessible website.
* Gather accessibility metrics during CI/CD process
* They started with [lighthouse ci](https://github.com/GoogleChrome/lighthouse-ci), then added axe-core via jest, cypress, or [playwright](https://www.npmjs.com/package/@axe-core/playwright)
  * They then converted it into a lighthouse score
  * Display lighthouse scores over time for each product
  * They have a "data lake" for their IT operations in AWS S3 and AWS Athena.  They put all the results into the data lake, then make dashboards.
  * They also have an Automated Compliance Platform (ACP), which opens jira tickets automatically if the score goes below a certain threshold.  Those jiras include a step-by-step process for recreating the issue/confirming the fix
    * The jiras might even have a "fix it for me" button, that automatically executes the steps in the ticket
    * The ACP already existed for security, because they wanted security findings to be actionable, not hidden in big PDFs of audit findings (avoid audit fatigue)
    * Stakeholders of ACP: internal compliance community (e.g. security people), developers, managers (who can see the SLA, dashboards, etc.)
    * They used to do external security auditing every 6 months, now it is every 2 weeks
      * they automated all the evidence collection that the external auditors will need
  * False positives are an issue.  The ACP already has the ability to make exceptions, so a ticket doesn't end up going to the team.  But the goal is if a control has _any_ false positives, they must revise or remove the control, because people need to be able to trust the ACP.
 
### Advancements in Indoor Wayfinding by Mike May, JR Rizzo, Kelly Lovett

* So many people rely on GPS for outdoor navigation, but there is no equivalent technology for indoor navigation
* One challenge is UX: people might be going directly somewhere, might want to browse to see what's nearby, need to include error tolerance (like how GPS can be a bit off)
  * If you are navigating to a specific location, you don't want a lot of point of interest information about what's nearby because it would distract.
  * Different if you are using a white cane vs. a service dog
* Grant from [NIDILRR](https://acl.gov/about-acl/about-national-institute-disability-independent-living-and-rehabilitation-research) for GoodMaps, NYU and [Open Doors Organization](https://opendoorsnfp.org/)
  * Open Doors Organization: travel and transportation accessibility organization.  They work with Amtrak on training, do wheelchair repair after the airlines break them, etc.
* Indoor positioning solutions
  * Bluetooth Low Energy: these are beacons that you install (some are battery-powered, require maintenance, but still work during a power failure) and they transmit. Low security risk.
  * Wifi positioning system, aka wifi fingerprinting.  Security/privacy regulations make this more difficult.
  * Ultra-wideband.  Low security risk.  Can be very accurate, down to the centimeter.
  * Visible Light Communication.  Uses LED modulation.  Requires direct line of sight from the selfie cam on the phone.  Many big box stores (e.g. Home Depot) have this for their staff.
  * Geomagnetic indoor positioning.  Accurate, but it requires pre-mapping.  Unlimited range.  Magnetometers on the phone. Minimal privacy risks
  * LiDAR (light detection and ranging).  Requires pre-mapping with laser beams!  Very accurate and good range.  Low privacy risks.
  * VPR (vision place recognition) -- basically matching visual features against the camera.  Privacy concerns around the image data transmission and capturing passers-by in the original photograph.
* Goodmaps provides additional information, not trying to replace a white cane or dog
  * It uses a LiDAR scanner -- they walk through the entire space and take the pictures
  * Camera Positioning Standard (CPS)
  * It uses the Apple format
  * They recently updated their UX so that it can be useful to non-blind users too
  * PDX airport uses it!  Also Michigan State.
  * They use the Apple indoor map format standard
  * All usage is anonymous, they don't collect any personal information about the user at all.  They do give statistics and route info to the customer sites.
  * They have separate apps for indoor and outdoor goodmaps -- eventually they want to combine them.
 
### Helping Organizations Grow Accessibility Maturity by David Sloan and Anne Scallan

* [Accessibility maturity slides](https://bit.ly/helpingmaturitycsun24)
* Maturity models help organization do 3 things:
  * Understand their current state
  * Identify their desired future state
  * Figure out the steps to get to that future state -- this is what the talk is about, in a series of case studies

#### Case study: organization that had accessibility audit result, but they didn't know how to prioritize them
  * Their goal was to publish a VPAT ACR soon that did not include any "Does Not Support" items
  * So they organized the issues as a draft VPAT
  * Issues were prioritized in alignment with the business goal of providing a VPAT to enable others to procure their services

#### Case study: organization had a few accessibility champions, but struggling to increase accessibility of products.  Testing was ad-hoc and could not be analyzed strategically
  * They created a ticket system, which allowed them to easily re-use remediation advice between tickets
  * They created a dashboard to show the tickets, and did a retrospective of the most commonly missed accessibility requirements in the past year

#### Case study: leadership was interested in accessibility, but product teams didn't have much knowledge
  * Weekly office hours
  * Product teams were able to shift left: addressing accessibility earlier in the development lifecycle, asking more advanced questions

#### Case study: client was getting regular audits (every other years), but weren't seeing much process
  * Incorporate automated testing into dev pipeline
  * Product teams don't have to wait 2 years to get feedback on whether their fix was good
  * Instead of having experts spend their time auditing, they focus more time on reviewing automated results with product teams and figuring out how to address them as part of the software development lifecycle

#### Case study: client had many products, each of which needed a VPAT ACR
  * Their procedure was inconsistent across products, also they wanted to add VPAT for European accessibility legal standards
  * They asked the people who wrote the ACRs what their challenges were, and then they re-wrote the procedures to be streamlined and in accordance with the relevant standard
  * This helped the organization start providing user-focused accessibility documentation, which helped the users who had been having a really hard time previously

#### Case study: organization had a good accessibility culture, but the subsidiary was very inconsistent
  * There wasn't a single person to talk to at the subsidiary at the organization, you had to talk to each product team, each of which had a different level of buy-in
  * They added a new position to the subsidiary: product manager for accessibility, who worked with all the teams

#### Case study: empowering teams to include disabled people in user research

* Organization wanted to do a usability study, but they did not have the internal capacity to design, recruit, moderate a study.
* The organization partnered with tpgi: tpgi explained what they did, and made decisions together.  Tpgi did a training for the staff about how they set up the study, what decisions they made and the impact they had.
* Staff from the organization were able to learn from what tpgi did, and built the skills to do the usability studies themselves in the future
