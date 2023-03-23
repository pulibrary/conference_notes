# Measuring ourselves: Github's accessibility scorecard

Link: https://www.deque.com/axe-con/sessions/measuring-ourselves-githubs-accessibility-scorecard/
Slides: https://www.deque.com/axe-con/wp-content/uploads/2022/12/Measuring-Ourselves_-GitHubs-Accessibility-Scorecard.pdf

Presenters: Katie McCormick and Kendall Gassner

Their challenges:

* Teams didn't know how to make their work accessible
* Feature teams unintentionally removed accessibility fixes
* Massive scale (number of PR's created each day)

Fundamentals program: it enforces three pillars: availability, accessibility, and security.  Fundamentals scorecards are prioritized over other scorecards.

Three a11y objectives:
* Audit progress
  * This one has multiple tiers - they have SLAs, which are tiered according to how severe the violation is (for example, the most severe bugs must be fixed within 35 days)
  * They have a GraphQL api that they can use to see if issues have been open for too long
* Static analysis
  * Unlike audits, this is more proactive.
  * Teams must use their linters
  * Teams can disable lint rules, but they get more points if they disable fewer rules/fewer times (gamifying it!)
  * they use `eslint-plugin-jsx-a11y`, `rubocop-rails-accessibility`, and `erblint-github`.
* Dynamic analysis (with e2e test data)
  * They just use axe-scanner
  * They measure how many possible url patterns have test coverage -- and teams with more coverage get more points

Since they added the accessibility scorecard, people are talking about accessibility and axe more frequently on slack, and more issues are getting closed!

Customer-reported accessibility issues are prioritized too, but they aren't part of the gamification.
