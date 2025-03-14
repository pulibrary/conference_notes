### Interpreting Accessibility Metadata for Inclusive Learning

Presenters: Charles LaPierre (from Benetech) and Madeleine Rothberg (GBH)

#### Accessibility metadata

  * Can be useful in discovery and procurement
  * Machine-readable information about accessibility features, accessibility hazards, WCAG conformance or EPUB specification conformance (and has it been certified).  Human-readable summary.
  * Can be found in an EPUB file.  Also as a separate ONIX file (ONIX 3.0 has much better accessibility metadata) or in MARC.

These metadata are now required in European law for ebook publishers

These are not just for books -- they can also apply to journals, anything online


#### Metadata display standards

* [Here is the new standard about how to display the metadata](https://w3c.github.io/publ-a11y/a11y-meta-display-guide/2.0/draft/guidelines/index.html#abstract)
* [Here is a publisher that displays the metadata according to the previous version of the standard](https://benetechaccessiblebooks.vitalsource.com/) -- search for an item, and there is an accessibility tab.

#### Library metadata

There is an existing [crosswalk document](https://w3c.github.io/publ-a11y/drafts/a11y-crosswalk-MARC/) (not for the new standard yet, that's in progress) -- currently, MARC does not have many accessibility fields, they are working to improve the situation

They are also working with NISO (a working group called EMMA?) to figure out a standard for how to describe materials that have been remediated (since the publisher's metadata may no longer apply to the remediated copy).


### Are Design Systems the Key to Sustained Web Accessibility?

Presented by David Cox

[Slides](https://dav-idc.com/csun/#tuesdays-session)

> Design system should be a first stop shop, not an one stop shop

The speaker did a study into whether having a really accessible design system translated into having really accessible websites.  The answer... not really. [Detailed results](https://docs.google.com/spreadsheets/d/1ecbgzRWHtr8RLkrxyIc1U9qkyjMo25ic3hKg3H8Fh2Q/edit)

* [Oobee command line tool](https://github.com/GovTechSG/oobee/blob/master/INSTALLATION.md#macos) -- it is a good tool for running the axe core rules (and some others) on a sitemap or list of URLs

#### Accessibility documentation in design systems

Design systems should have an accessibility page:
* what commitments do we have to accessibility (compliance level, etc.).
* What are the known issues?
* What is the accessibility strategy for this Design system?
* What Accessibility benefits does using the design system give to a product team?
* What work does the product team still have to do in their product for accessibility even when they are using the design system?
* Don't include general web accessibility info that is readily available elsewhere (or just link to it)

The documentation in a design system is a product, with product teams as users, you need to test if it is effective 
