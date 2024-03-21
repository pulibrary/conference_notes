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

* [Angular Slides will be available on the CSUN web site](https://www.csun.edu/cod/conference/sessions/index.php/public/presentations/view/1726)
* General problem: you want to use a 3rd party component, but don't want to be locked in to their accessibility bugs
* Attribute directives can help create consistent accessible experiences while preserving extensibility
* This talk is specific to Angular, though other frameworks have similar tools and structures
* Angular has components and directives.  Directives can be attached to a component or a DOM element to change its behavior.
* The project was to re-implement the UI of an entire platform in just a few months, in advance of an important accessibility audit
* They wanted to avoid "Accessibly but inconsistent": every widget works individually, but the controls and behaviors of each widget are different and unpredictable
* They started with [ng-bootstrap](https://github.com/ng-bootstrap/ng-bootstrap)
  * It claims that "all widgets are accessible", but it definitely has some accessibility shortcomings
* One approach: wrapper components
  * They would create a component that contains the ng-bootstrap one and fixes its accessibility issues
  * Limits configurability and extendibility, have to build each use case into the same component
  * You have to reimplement all the same `@Inputs` (props for Vue) from the ng-bootstrap component on the wrapper component
  * Nesting these wrapper components can become unweildy
* So instead, add attribute directives to the ng-bootstrap component
* Example: pagination
  * the ng-bootstrap component had most of what they need: `role="navigation"`, it is marked up as a `<ul>` with `<li>`s, it does aria-current
  * But it has some problems:
    * causes a weird scroll on screen width of 320 pixels
    * it does not announce page changes
    * the component had some options that were considered harmful for usability, so they wanted to prevent developers from using those options
  * They used the [`AfterViewInit` lifecycle hook](https://angular.io/api/core/AfterViewInit), and had a bunch of methods to modify the DOM according to their needs with the [Angular renderer](https://angular.io/api/core/Renderer2)
* Dropdown menu
  * they keyboard interactions were all wrong
  * they wanted to implement a specific aria role
  * They again created a directive that added event listeners and modified the DOM through the renderer
* They created a lot of documentation for their directives, but if the engineers don't read the docs...
* How do you make sure developers actually use those directives?
  * There was no linting, people did definitely forget to do the directives, or used the wrong one.  It was mainly a lot of communication
* They did create some wrapper components.  For example: ngb's datepicker and timepicker needed accessibility work, but they are always used in the exact same way, didn't need any config options, so might as well just create a component.
* Question about performance: they didn't measure performance impacts, but the old version before the migration was really slow, so it was a performance improvement overall

### Analysis of Campus Disability Support Center Websites by Lesley Farmer

* [Campus Disability Support Center websites slides](https://tinyurl.com/dscwebsites)
* None of the sites were fully accessible.  Issues included videos without captions, etc.  A lot of those are because of the larger campus site, or because they are stuck on an old system, or in the middle of some migration.
* Recommendation: test your disability services website with users with various disabilities.
