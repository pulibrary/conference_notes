### KPIs for accessibility by Kate Kalcevich

* KPIs = key performance indicators
* When you are working with a large scale of web pages (e.g. 15,000 pages on a provincial government website), how do you know if you are getting better or worse at accessibility?  There are challenges when you are taking a compliance approach to your reporting.
  * How do you measure progresss if just one page is inaccessible, or if it's uneven between departments?
  * The approach was to self-audit, which is a limitation -- not consistent
  * How do we know if we're getting better if we're just checking against WCAG?
  * Also, if you wait a year between each audit, and then get hundreds of issues to fix at once, it's not very actionable for the teams who have to do the work.
  * Also, something can be completely WCAG compliant but not very usable.
  * And the accessibility guidelines don't actually include everything people need (e.g. dark mode is very useful, but it's nowhere in WCAG).  Also, having too much white space can be very difficult for someone using a screen magnifier, but WCAG doesn't cover that either.
* Another approach: figure out the core tasks, and see if screen reader, screen magnification, and voice control or eye control users could complete the tasks.  Then the metric is how many people could just complete the task.
  * This is an easier approach to measurement, and focuses more on the outcomes
* Trying to make everything 100% accessible all at once is overwhelming, need a way to prioritize
* The KPIs are focused on Product, People, Process.  They help you find gaps in your processes.
* Introduce just a few KPIs at a time, then add.  Make sure that the KPIs make sense in your culture.
  * People KPIs:
    * Do teams have the skills?
    * Do they have the time to do accessibility work?
    * Do they understand user accessibility needs?
    * Are teams incorporating accessibility in their work?
    * To measure these: surveys, observational studies, time tracking/story points
    * Example: 90% of new team members finish accessibility training in 6 weeks
    * Example: 60% of digital team members engaged with a user with a disability about the product in the past year
  * Process KPIs:
    * Number/severity/time to fix issues
    * Automated test coverage
    * How often and how much of your interface has been studied in user testing
    * How much has your design system been studied in user testing, and how much is your design system used in the products?
    * Example: 90% of the design system has accessibility documentation
    * Example: 80% of new features are tested for accessibility before release
    * Having a good design system and wide adoption of it seems to be a big sign of maturity here!
  * Product KPIs:
    * Compatibility and usability (task completion)
    * User satisfaction
    * Focus on a specific technology (e.g. screen reader accessibility), class of issues (form inputs not labeled), or important feature
    * Example: All new features attain an average [AUS](https://makeitfable.com/accessible-usability-scale/) score of 68
* Teams should set KPIs in coordination with leadership, so that they can report on things that the leadership recognize as important to the organization 
* [Accessibility Usability Scale (AUS)](https://makeitfable.com/accessible-usability-scale/)
* [Canada Post Mercury design system](https://design.canadapost-postescanada.ca/en/mercury/components/breadcrumbs.page#!navtabd2049073e25) has comprehensive accessibility documentation

### Standardizing Accessibility with Angular Directives by Brian Glidewell
