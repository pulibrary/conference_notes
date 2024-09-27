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


### Learning from Past Security Breaches: Strengthening AppSec Efforts and Focus by Jon McCoy


### I Know What You Did Last Summer: Lessons Learned from Privacy Breaches and Scandals by Dr. Kim Wuyts
