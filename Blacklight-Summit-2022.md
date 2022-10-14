Blacklight Summit ’22 | Cornell

Open source collaborative platform for building discovery solutions

Support for: rails 7, solr 9, Bootstrap 4/5

Blacklight committer calls
Every 3rd Wednesday at 2pm EST

Blacklight-Adjacent Applications

Spotlight = curated digital collections
Spotlight is for exhibits

ArcLight = archival material and EADS

GeoBlacklight = geospatial data and maps
https://github.com/projectblacklight/blacklight-maps

Samvera = Digital repositories, where Blacklight is used in the hyrax/hydra-head gems in powering search
Hyrax is for a repository (Hyrax is part of the Samvera community)

Apache Solr = Search platform that Blacklight uses to power its search tools and document display of results

Apache Lucene = Set of Java search libraries that powers Solr and ElasticSearch

QQ: 
Does Blacklight utilize iiif resources for image implementation? Would iiif API be “compatible” for such features to properly function? 

Live Presentations: 

Miriam Campos-Quinn , John Lowe | Ephemera Presentation 

https://cinefiles.bampfa.berkeley.edu/

Hearst Museum of Anthroplogy

https://portal.hearstmuseum.berkeley.edu/

collection.bampfa.berkeley.edu

https://cinefiles.bampfa.berkeley.edu/catalog/61386

QQ: How are the resulting links (ex: of other works of the artist) displayed/ranked? (According to relevance, popularity?…)

Eben English | Boston Public Library

digitalcommonwealth.org

Digital Collection Site w/ different types of content

Provides digitization services from a collection of different libraries

Blacklight-maps: can view search results (geographic data) displayed on a map

gem used: Blacklight iiif search (makes manifest available to allow for additional features of content displayed)

Interested in full-text search content for users, better implementations of solr (may chat w/ Eben)

Phillip Robinson/ Huda Khan | Cornell University

https://docs.google.com/presentation/d/1Soc847D4LbZNRd6UGPCs-rQ26_6rnwXvrtyePAd_Hvs/edit#slide=id.p1

FOLIO: Bibliographic metadata

EBSCO Discovery Service: articles search

CUGIR: GeoBlacklight

DSpace: eCommons institutional repos (theses, scholarly articles, etc)

Wikidata linked records made possible through Blacklight

Sean Aery | Duke University

5 apps that use Blacklight:
Catalog
DigiRepo (Public)
Research Data Repo
Collection Guides
DigiRepo (Admin)

TRLN Shared Engine (Triangle partnership)

Upgrades from BL6 -> BL7

Took about 2 months focused dev team attention per app

Complications included customizations, Bootstrap major updates to code-language

Bess Sadler, Carolyn Cole, Jane Sandberg, Anna Headley | Princeton University

https://docs.google.com/presentation/d/1IdHov-sbl_zIngHemWOs-eGY5Oq_al5nLvHxkraf9cY/edit#slide=id.g15d90492039_0_44

datacommons.princeton.edu

Migration from DSpace -> PDC Discovery (integration w/ Blacklight)

Jumpstart methodology: not starting from a blank state

Migrate/ Redescribe Research Data in PDC Describe (Dublin Core metadata outdated)

Migrate DataSpace content to Figgy

Traject config (indexing) (de-duplication)

DSpace: used for XML indexing

Utilizes rails-template and Blacklight to jumpstart migration

Jane: Change The Subject

Make MARC records (terminology) less offensive for patron view. Records (both old and new) are indexed so that search results still return 

Anna: ArcLight app / Finding Aids Website

findingaids.princeton.edu

Patrons are able to submit form through collection sites for new, improved and preferred terms

LCSH (Library of Congress Subject Heading)

Johnathan Rochkind | Science History Institute

Template is going for a “brochure” informative formatting

Built on active record models from their db

Goal is to write an application similar to a rails app for more customization

Enables description, transcription and english translation tabs for records 

OHMS Oral History Metadata Synchronization (enables to hear transcribed text)

KITHE gem: db metadata records that ends up integrating with Blacklight and solr 

10.4.22

Improving Hyrax Bulk Imports By Customizing Bulrax

Brad Watson | Emory University 

Digital Repo Software, Ingest time are slow and errant

Possible solutions: 
Bulkrax*
Upgrading Hyrax
Diagnose/fix failing jobs from production log

Incorporate Hyrax overrides (FileSetActor/AttachFilesToWorkJob)

Importation was associated to db object that retains Entry instances that directly associate to the ActiveFedora object created. 

Creating a Sidekiq Job that pulls the FileSet object and its parent Work from entries retained by the Importer Object

Condensed uptime of ingest time from 11 hours to approx. 1 hour

Michael Kanning | University of Penn

Philly Area Consortium of Special Collections Libraries / Penn Libraries

EAD: Encoded Archival Description Finding Aids discoverable from regional institutions

Expertise in Ruby on Rails/Blacklight apps

Created app that has feature parity and potential for incremental improvements

ArcLight does not provide inventory-level discovery, does not offer control over harvested EAD (metadata), and makes user wary of light development 

Methodal quackery / search results 

Learning EAD can be difficult 
ViewComponent learning curve
Harvesting directly from ArchiveSpace using Docker (v. FTP)

Aggregation time is now at about an hour

Searching and faceting functionality is feasible to follow 

Uses ruby 3.1.2, Rails 7 and BL 7.26

Bill Dueber | University of Michigan

Analyzing string in solr

Centralizes code (solr stringtype) 
Solr TextField allows for NLP (tokenization, etc)

Looking to solve the problem of author browse and providing user input 

Allows for alphabetical list of searched author along with other authors (called an AuthorBrowse)

Author = committee, conferences, etc

&try_to_deal_with_cjk; 

Range queries do not run the analysis chain of a textField* 

A solr string type mirrors this 

ICU latinization (?)

Your index and query transform must match

Browsekey Analysis 

Keyword tokenizer creates one big token

Restrictive analysis (?)

David Kinzer | rspec methods 

Line10 indentation of integers (22 4500)

running a test produces an error regarding MARC fields 

without_partial_double_verification

allows the passing of this test.

Wrapper for a traject (indexing) library…

binding.ply(?)

rspec ‘matcher’: relishapp.com

jar (files)(?) Anna H.

John Lowe | UC Berkeley

BL: solr index (apache lucene) docs index created, BL provides interface to “discover” indexed items (BL API?)

Hector > solr-for-newbies > tutorial for simulating 

CJK text-type? https://www.google.com/search?client=firefox-b-1-d&q=solr+text_cjk

https://solr.apache.org/docs/3_6_2/doc-files/tutorial.html

Search Builder: how solr passes/parses queries to solr, and the process of overriding this process

vim apps/model/search-builder.rb

when querying in solr, parameters will get called in order (according to default processor chain)

at this stage, you have access to BL/solr parameters (here you can customize search filters and create overrides)

Search service will grab the parameters and run the search. 

What are the implications with what we have learned / been exposed to for PUL??? Anna, Bess, Carolyn, Hector, James

￼

and, in words: search service pulls together 2 pieces: a search builder that converts user params (or other context information) into solr query parameters, and the repository connection (which knows how to send + receive solr responses)search service provides a consistent interface for controllers and other classes to request data from solr (with handy methods for a search, single document, and a couple specialty queries)---

David Kinzer | BL on Rails

BL = a Rails engine 

blacklight/app

contains controllers, config, spec, model, etc (composition of a Rails app)

In gemfile > there is a BL gem integrated (looks like its own app)(app within an app) 

a rails engine is an app that can be configured and packaged and serviced as an app service within itself. 

Assets (JS, CSS)
Webpacker changes have occurred 

Styles are setup within this folder

BL plugin: a Blacklight plugin is basically a gem specifically designed to work with Blacklight.

vite (veet): feature-rich, feasible to deploy. Similar to jsbundlr, more streamlined regarding running alongside sprockets, config files are easy to read. 

Provides module reloading, combines JS and CSS

Webpacker -> ES build

jsbundling-rails with esbuild

vite provides sourcemaps for SAS to work with it

How to build assets: ruby builds into rails, rails hooks into a development server

Import maps: feature in rails7, way of managing JS (dependency management system) 

[PUL] We upgraded our catalog from webpacker to vite primarily because of webpacker being deprecated and relying on old versions of JS libraries.  Still using sprockets though.

Q: What app features does PUL BL/solr amalgamation have, where would we like to be, what features would we like to see integrated? 

PUL roadmapping

How to build a “formulaic” roadmap

mozillasciene.github.io/roadmapping


Q: prospect/outlook for solr/BL tech consultant?? (upgrading deprecating, migration, etc)

Eric Pugh | querqy.org

Open source project that adds common search control to solr

Library that allows query re-writing

Relevancy tuning demo 

“fine-tuning” search results (Ex: eCommerce site lookup: notebooks)

Search Management UI | SMI

Nikitas Tampakis | BL Plugins - Add-Ons Session (Arc/Geo/Spot)
Sean Aery (ArcLight)

Initiated at Stanford

Community-development sprints created for MVP construction

Finding aids solutions driven product

Stanford working on maintenance for updating Arclight as many of the experts are no longer active on project

Spotlight/Starlight 

github.com/projectblacklight/spotlight

Q: Spotlight seems like a “prettify” for interface, not much emphasis on development for this application

GeoBlacklight

github.com/geoblacklight

geoblacklight.org

Eliot (PUL) attends geoblacklight monthly meetings 

Q (Bess): What is a “committer” role, format of committer calls, etc.

Benjamin Arminton | BL & Ecosystem

Can serve as a discovery front-end within a larger infrastructure

Multiple data and metadata workflows may intersect in a BL instance

Blacklight can also serve as a way to retrieve data and metadata (in addition to discovery) 

Bento-box interface for BL, presents bucketed results to a user

Q: more overview of bento-box structure of BL (search-engine conglomerate)

Q: David Kinzer: OAI Processing platform/workflow

Ingestion through PUL, because it is contained within a separate workflow, able to import data from the ILS

Q: ILS? Voyager to ALMA? 

Q: How do you change the ruby versions required/compatible with an application (Ben Armintor)





