# SmashingConf New York 2024 - 10/9/2024

## Life Is A Mystery… by Scott Jehl

* CruX: [Chrome UX report](https://cruxvis.withgoogle.com)
* [performance-inequality-gap-2024](https://infrequently.org/2024/01/performance-inequality-gap-2024) 
* https://web.dev/articles/vitals
* [mv-initial-load-times](https://www.filamentgroup.com/lab/mv-initial-load-times) 
* [the-cost-of-javascript-frameworks](https://timkadlec.com/remembers/2020-04-21-the-cost-of-javascript-frameworks/)
* [will-serving-real-html-content-make](://www.catchpoint.com/blog/will-serving-real-html-content-make)
* [spectrum-web-components](https://opensource.adobe.com/spectrum-web-components/)
* CSS & Shadow DOM 
* [introducing-popover-api](https://developer.chrome.com/blog/introducing-popover-api)
* [rfc-customizable-select](https://developer.chrome.com/blog/rfc-customizable-select)
* [ollama](https://ollama.com/)

## The Secret Mechanisms of CSS by Josh Comeau

### Flow Layout
* Analogy
* Constrained horizontal space, unlimited vertical space
* The layout is built within blocks
* Images are considered inline elements
* `inline-block` sits like an inline element. Creates a rectangle
* `inline` line-wrap . will not create a rectangle

### Flexbox layout
* Items are distributed across the primary and secondary axis

### Positioned Layout
[Resources Josh Comeau](joshwcomeau.com/smashing)
* Elements are anchored to something other than its calculated layout.
* position
   * absolute - child items look for nearest parent element with 
   * relative
   * fixed - elements anchor to the viewport
* z-index
   * works in combination with position
   * implemented in some not all layouts
   * positioned elements will be promoted above non-positioned elements
   * z-index compares values within the same stacking context

## Generating the Future by Tejas Kumar
### Types of AI
* [Latent Space](https://www.latent.space/)
* [Attention is All you need](https://proceedings.neurips.cc/paper_files/paper/2017/file/3f5ee243547dee91fbd053c1c4a845aa-Paper.pdf)
* [tej.as podcast](https://tej.as/podcast)
* [ask lukew](http://ask.lukew.com)
* [datastax](https://www.datastax.com/)
* [v0.dev](https://v0.dev/chat)
* [LLM-as-judge](https://arxiv.org/abs/2306.05685)
* [Designing Data Intensive applications](https://www.oreilly.com/library/view/designing-data-intensive-applications/9781491903063/)

* Rule-based
* Predictive
   * e.g. autocomplete on your phone
* Deep Learning
   * GPT model is based on: [Attention is All you need](https://proceedings.neurips.cc/paper/2017/file/3f5ee243547dee91fbd053c1c4a845aa-Paper.pdf)  

### Problems with GenAI
* Knowledge Cutoff
* Hallucinations
* Finite Context Length
* It's not human

### RAG - Retrieval Augmented Generation
* Components of RAG
  * Data
  * Embedding Models
  * Vector Store
  * "The AI doesn't matter. What matters more is the UX and the frontend."

### Generative UI
* [Movies++ research project powered by DataStax](https://github.com/datastax/movies_plus_plus), uses semantic search.
* UI itself is dependent on inputs either by users or application developers beforehand.

## Bridge the Gap between Design and Development, One Token at a Time by Samantha Gordashko
* [More resources - Samantha's website](bento.me/samiam)
* Design token
   * Expresses a design decision
   * Design Tokens Community Group
   * Name, Value, Type, Description. 
* [tokens-studio-for-figma](https://www.figma.com/community/plugin/843461159747178978/tokens-studio-for-figma)
* Consider Devs as users.
* Lack of knowledge on both sides contributes to the GAP
* Accountability for your role on the team.
* Be willing to learn and have empathy
* Documentation + Cross functional communication
* Collaborate with the engineering team
* Iterate back on what we have worked on.

### Design Tokens Tools
* [penpot](https://penpot.app/)
* [Blender](https://www.blender.org/)
* [Figma](https://www.figma.com/)
* [Framer](https://www.framer.com/)

## Managing Design Systems, from Features and Releases to Roadmaps and Backlogs by Nathan Curtis
* [Managing Design Systems (Smashing NY 2024)](https://speakerdeck.com/nathanacurtis/managing-design-systems-smashing-ny-2024?slide=95)
* [Designing a community driven Design System](https://www.youtube.com/watch?v=4MpGxmlOf7w)

### How do we produce features (made - documented - released)
* Design tokens
* UI componenents
* UX patterns
* Content guidelines

### Task
* Plan
* Scope: Understand what we want to make, why, and it's worth it
* Design
    * start, make, test, share, review, deliver
* Specification - Design spec or spec
    * A document that describes the design, handoff or final production
* Code
    * Start, make (Draft API, ), test, share, review, deliver
* Code docs
* Figma asset
    * Start, make (Obtain API feedback), test, share, review, deliver
* Design docs 

### Releases
* Orchestration
* Release

### Initiatives
* Problem statement, outcomes, outputs

### Boards
* Dev Intake:  Support request, Defect, Feature request contribution proposal
* Design Intake: Feature request contribution proposal, Defect, Support request

## (Lost) Found in the Details by Jessica Hische
* [Lettering artist and author](https://jessicahische.is/)
* [Logo evaluation process](https://bit.ly/logoevaluation)
### Brand Equity 
* Logotype
* Mark
* Color
### Refresh vs Rebrand
* Refresh
* Rebrand
    * Company pivot or significant change in offerings
    * Aggressively target a new audience
    * Never actually had a well articulated voice & vision
### Typography
* Scalability
* Usability

### Timeless Logo
* It remains in continual use for a very long time
* Avoid gimmicky design
* Attention to detail

### Process
* Learn client goals
* Discuss game plan for complete brand identity
* Evaluate existing design and decide what's worth keeping
* Create the scope based on goals, collaborators and budget
* Begin broad and narrow scope with each round
* Discuss alternate versions and next steps
* Be a resource for the brand team moving forward





