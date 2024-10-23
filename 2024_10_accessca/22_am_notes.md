# Access Conference

#### Living and Working with AI

* deflationary view of AI
* Will we achieve generalized intelligence
* Intelligence is not a single dimension.
  * reasoning is different from
  * Vision
* From AlphaGo (2016) beat Lee
* The dominant paradigm of deep and machine learning
  * this superceeded logical programming
  * they use neural networks
    * this tracks patterns in a large dataset
    * classify objects categorically
      * facial recognition etc
    * these patterns are then generalized
      * makes them useful in a new environment
    * Extremely skilled mimics in when deployed in a new environment
* Their outputs are ALWAYS probabilistic
* It is stochastic
* These are not logical inferences
* AI tries to learn from the dataset
* Recommender systems are also used in machine learning
  * can we state this explicitly. Our recommender system used the following rules
  * Generative AI. They create content (text) or images
  * in a genomic dataset the AI can be used to predict the probabilistic potential of what a protein will look
* They learn by processing (inductive learning) individual points and generalizing them
  * They will have difficulty with data on the margins
  * stop assigning human attributes to machine learning (hallucination)
  * ML will make things up. We don't -yet- have a principled answer to this
    * we address this post-hoc
    * reinforcement training by way of humans which is fed back into the training

* The ML can misled people who are not domain experts
* As epistemic agents we have many ways that intelligence will manifest
  * we can reason our way through problems
  * where there is a causal law
  * we can reason from abstract principles
  * AI systems lack genuine embodiment
    * we are embodied and embedded

#### Beyond the AI Hype: Deploying and Evaluating a Conversational Agent Using LLMs in an Academic Setting

**Joshua Chalifour**
**Francisco Berrizbeitia**

* Build a retrieval augmented generation
* Funded by an internal seeded grant from the library
* Stack that powered
  * Indexing to create knowledge bot
    * done via scraping the website (everything)
  * The user performs a search that query the LLM
    * this is then fed to a vector database which generates and knowledge base
    * this is a manual process of re-training the LLM model
      * based off OpenAI 3.5 and Gemini
* Came up with 14 prompts
  * the answers were judged based on information found in the library

#### Beyond Research Data Deposit: Inside the Preservation Efforts of Borealis

**Meghan Goodchild**

* How to migrate from documents from proprietary formats to open ones
* Borealis is funded by the Canadian Govt.
  * Hosted at UT and based on Dataverse
  * Spaces are managed by individual libraries
* All files are checksummed
* File format identification including size etc.,
* Also does format normalization to future proof the data
* Ontario Library Storage Research Cloud
* have a fixity checking for remediation and bit rot
  * checked over 200K files
  * long process that tooks over 50 hours
  * Scholars Portal paid for Archivematica integration to help users created additional data preservation

#### Performance testing data repository infrastructure involving Fedora 6.x in a High Performance Computing (HPC) environment

**Arran Griffith**

* Texas Advanced Computing Center (TACC)
  * grant allocated testbed environment including hardware specialists responsible for maintaining the infrastructure
  * Provided open-access data from NSF-Funded, DesignSafe Data Depot for testing
  * The test data was not the write-once and read many
* Tried to test the hard limits of what would break
* Also wanted to provide Cost Analysis
* Original plan was testing to failure
* Shifted to ingest execution time
* This was a shared HPC which meant the work load would restrict when it was available for testing
* This was a deeply nested hierarchical system (revealed positive first results)
  * showed improvements over Fedora 5
* OCFL helped with file locking
  * Still more work to do

#### Digital Asset Management for Reference Libraries, Galleries and Museums: A Case Study and Demonstration

**Kristy von Moos**
**Catherine Campbell**

* A clearly defined strategy around internal harm reduction
