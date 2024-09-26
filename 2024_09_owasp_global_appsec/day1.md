
### Thriving in the Age of AI by Aanchal Gupta

Quote: "There is a lot on our shoulders when we introduce AI into our systems"

#### Vulnerabilities of Inference Mechanisms

XPIA - this is not a solved problem.  You need to validate the input and output, even though these can be bypassed. The best thing is early detection. 
query attack
inference attacks
contextual maniuplation

##### mitigation
making sure that ai agents run at the appropriate permissions, can't access or infer any private data
also rate limiting


#### Vulnerabilities of feedback mechanisms

Feedback manipulation to mislead the model's performance (make sure to validate feedback by humans first)
Targeted adversarial inputs (introduce targeted attacks via feedback)
model collusion -- keep models separated from each other

#### Vulns of ethical and safety measures
bypass moderation
bias exploitation

continuous monitoring, human in the loop

#### Using AI for security

When an incident happens, security analysts have to query 10-20 different monitoring platforms and data sets.  Plus there may be relevant data in other data sets that they don't yet have access to.  Microsoft is using AI to automatically query these systems for them, and to automatically grant access to the data they need just in time.

### Striding Your Way to LINDDUN: Threat Modeling for Privacy by Shanni Prutchi and Chris Bush

Threat model: 4 questions
* What are we working on?
* What can go wrong?
* What are we doing about it?
* Did we do a good job?

STRIDE - an acronym to help you with the "What can go wrong?" question to identify security threats
* Spoofing
* Tampering
* Repudiation
* Information disclosure (privacy breach or data leak)
* Denial of service
* Elevation of privilege

Data privacy depends on data security, but goes beyond.  It doesn't just concern itself with the active users of the application, but also any individual whose data we have.  It is contextual too -- just because a data point is available in one data set doesn't mean that it is okay to disclose it in another context (e.g. having an email address registered for an account is different than having that exact same email address registered for a more sensitive site).

LINDDUN - you can use it with the 4 questions, just like STRIDE
* Linking - learning more about a person or group based on associating multiple data points through identifiers
* Identifying - learning the identity of an individual when doing so is not intentional.  This can happen through leaks, deduction, or inference.
* Non-repudiation - the system retains the ability to attribute a specific action to a specific individual
* Detecting - deducing an individual's involvement through observation (for example, if you log in to a sensitive website with somebody's email and a bad password, and the system doesn't log you in but still confirms that that email address has an account on that site)
* Data disclosure - excessively collecting, storing, processing or sharing personal data. 
* Unaware and unintervenability -- not informing or empowering individuals that their personal data is being collected and used
* Non-compliance - not following best practices or legislation

[LINDDUN GO is a card game](https://downloads.linddun.org/linddun-go/default/v240118/go.pdf) you play to do the privacy threat model 

They used an integrated library system as an example for this framework!  Fun!

How do you mitigate threats?  With Privacy Enhancing Technologies (PETs) -- some of these sounded really interesting!  They didn't go into a lot of detail, I'd like to learn more.