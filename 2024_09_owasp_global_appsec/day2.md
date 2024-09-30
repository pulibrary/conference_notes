### Red, Blue, and Purple AI by Jason Haddix

interesting ai bots mentioned
* spear phishing -- given the name of an individual, it will write an email that is super convincing to them (security experts say "yeah, I probably would have clicked on that").  Very scary!
* XSS filter bypass -- when you think you have fixed an XSS vuln, it will give you some other curls to try to verify that you _actually_ fixed it
* during incidents, help give you checklists of things to check so you don't forget during the stress
* create wireshark filters to find what you actually want
* creating new DAST and SAST rules (like a semgrep rule)
* stridegpt: it does threat modeling for your application

### Sanitize Client-Side: Why Server-Side HTML Sanitization is Doomed to Fail by Yaniv Nizry

* Example of XSS payloads that bypass server-size sanitizers:
  * HTML4 vs 5. Sanitizers typically parse the string, then remove the bad stuff.  However, 4 vs 5 has different syntax (e.g. comments are different).  If the sanitizer parses as HTML 4, the attacker can use a HTML 5 payload to bypass it.  The example given was a real-life application that used a third-party sanitizer based on the PHP built-in parser, which before PHP 8.4 relied on libxml2, which does not support HTML 5.
  * Different browsers have different HTML parsers
  * HTML is an evolving language, the sanitizer might not be up to date

Recommendation
  * [SanitizerAPI](https://sanitizer-api.dev/) (behind a feature flag in firefox, chrome is rolling it out).  This would mean that it would use the same parser that the browser uses, without needing to re-parse.  In the meantime, there's also https://www.npmjs.com/package/dompurify.

### Millions Of Public Certificates Are Reusing Old Private Keys by Dylan Ayrey and Joseph Leon

* They found that 10% of certificates were created using the same private key as another cert
* https://crt.sh/ is a central log of all tls certs that have been issued -- this is where they got this data (by searching for the public key).  CAs must log here, or else the browser will give an unsafe cert alert
* They focused on certs that had been revoked.
* They gave a story: developer accidentally commits the cert's private key to version control, they revoke the cert and put out a new cert using the same private key.  The revoking/new cert was essentially useless in this case, since a bad actor could still decrypt all the traffic.
* cert-manager.io and acme.sh -- two popular cert managers -- reuse the same private keys always unless you otherwise specify.  certbot, fortunately, creates a new private key each time.  They believe that this automation is responsible for much of the reuse.
* Their recommendation: don't reuse private keys to make new certs.  Don't reuse them to make new certs for different subdomains.
* This only is a security issue if the private key is leaked.  But they found that some large companies reuse the private key for 10 years -- so it is not impossible that they key is leaked somehow during that time.

### Learning from Past Security Breaches: Strengthening AppSec Efforts and Focus by Jon McCoy

Emphasis on putting runbooks in place _before_ a security event.  And blameless post-incidents meetings.  And supporting new members of the security community.

### I Know What You Did Last Summer: Lessons Learned from Privacy Breaches and Scandals by Dr. Kim Wuyts

* Example: vending machine with facial recognition.
  * "The lawyers said it was GDPR-compliant!" -- maybe yes, probably not, but either way compliance is overrated.
  * The lesson: We need privacy engineering, not compliance
* Example: period tracking apps after the supreme court overruled Roe
  * The lesson: Privacy impact depends on context (before or after a court decision matters!)
  * The other lesson: linkability (things can be deduced from combining different pieces of data)
  * Privacy is not a pseudonym for confidentiality.  Privacy also considers linkability, for example.
  * A single feature does not happen in a vacuum.  It exists in a whole privacy ecosystem, the same feature has different implications in a different business context.
  * Diverse teams with diverse viewpoints
* Example: Strava gave away location of secret US army bases
  * lesson: deidentification is not easy.  Anonymization is impossible -- ongoing research topic, don't try to invent your own unless you are an expert
* Example: [meta using all personal information to train AI](https://noyb.eu/en/noyb-urges-11-dpas-immediately-stop-metas-abuse-personal-data-ai)
  * lesson: the original purpose of the data matters, using it for a completely different purpose may not be okay
  * In data privacy, there is not a concept of who owns personal data.  If the data is about you, you are the "data subject", which does give you some rights, but you don't own it.
* Example: [pay or okay](https://noyb.eu/en/noyb-files-gdpr-complaint-against-meta-over-pay-or-okay)
* Example: Pokemon Go.  When it was first rolled, out, there were pokemon in random individuls' yards, so users would just go into other people's yards to catch them.
  * Privacy as a whole goes beyond just data.  It can have an impact beyond the online world.
* Example: Mozilla's study about car privacy
  * [Tesla workers shared images from car cameras, including "scenes of intimacy"](https://arstechnica.com/tech-policy/2023/04/tesla-workers-shared-images-from-car-cameras-including-scenes-of-intimacy/)
  * [Ford seeks patent for tech that listens to driver conversations to serve ads](https://www.pcmag.com/news/ford-patents-in-car-advertising-system-that-listens-to-passenger-conversations)
  * We need to strive for Transparency, Intervenability, Unlinkability
* Example: Microsoft Recall
  * The database was insecure
  * If multiple users use the same device, they have no privacy from each other
  * Currently it's stored locally, but no guarantees
  * Even if it had been secure, it would not be private
* Example of app that violated privacy by design -- after initial critiques they said "don't worry about it, we just moved it to AWS so it's secure"
  * Privacy enhancing technologies aren't magic crypto dust, they can't fix bad design

New area of research: Transparency enhancing technologies (automatically making sure privacy notices, cookie notices are understandable, simple, and actually accurate to the current state of the system)

Don't aim for perfect privacy.  Start small and evolve.
