## ElixirConf US 2024 (Orlando) Highlights and takeaways

### Training: Instrumenting elixir applications
  - a good training, well-facilitated by Ethan and Zack. went through motivating use cases for instrumentation, telemetry techniques provided by erlang directly, and the Telemetry elixir library. working through the examples was a good exercise not just in these concepts but also in working in and with idiomatic elixir and phoenix projects.
  - this is the sales site for this training: https://www.instrumentingelixir.com/
### Livebook
  - There were a lot of talks about livebook, this seemed to be the theme of the conference. I mostly didn't go to them, except the opening keynote. Demos similar to the one Michael Klein did for us, connecting to a remote machine and executing code in that context.
### Broadway
  - There were a few talks about broadway that I attended but they were mostly concerned with either scale we wouldn't dream of, tooling we don't use (e.g. broadway with the rabbitmq producer), or other extremes in the problem space.
  - In my conversation with Eric Saxby he cautioned against using updated_at as a way to trigger our pipeline. He said he has found that teams end up in a scenario where they write some new process and then realize, oh, wait, that doesn't actually need to trigger our pipeline. Something to potentially watch out for.
### Testing
  - "Phoenix test" wraps some other testing libraries to give a more consistent test interface between controller tests and feature tests
    - talk was Testing phoenix apps (German Velasco)
  - I chatted with Eric Saxby who showed me some test setup stuff he does on his team using test tags. Here's his blog post: https://www.livinginthepast.org/blog/exunit-tags-test-setup/
  - I missed "A11y testing your phoenix liveview application with Excessibility" because I was in a conversation but I think the title says it all, may be interesting or useful. I will try to go back and watch the video.
  - "Beyond Mocks" speaker Nicholas Henry argued that the negatives of test doubles outweigh the positives of separating test code from production code
    - they lead to false passes and false fails: a change to the wrapper invalides the mock, and the wrapper and mock can fall out of sync
    - they are outside the usual flow, they are "solitary and interaction-based" instead of "sociable and state-based" (I didn't really understand this)
    - They contribute to design fatigue
    - proposes using "nullable" pattern instead, which is basically a switch inside production code. Then you have to chain that switch through all the callers of that code. Seems annoying even if there's only one code path to your external service, seems like a mess if there are multiple modules using the client in question.
    - He said the goal of this talk was to make us more aware and thoughtful when we use mocks, not necessarily convince everyone to use this pattern.
  - "more testing, fewer tests"
    - Pretty good presentation of a few different kinds of testing strategies. He has a library called "parameterized_test" which seems cool for simplifying the comprehension of policy-type test scenarios like the ability tests he used as an example. Allows you to write a table of permissions rather than huge lists of test cases.
    - Also talked about property-based testing and snapshot testing, use cases for each of these types of tests
    - slides (but note these were heavily interspersed with code examples from his editor, so if you want this info I'd say watch the talk): https://tylerayoung.com/assets/files/more-testing-fewer-tests.pdf
### Security
  - "securing the future" talk analyzing various potential vectors of security threat to the elixir ecosystem.
    - Mentioned using trivy to scan containers.
    - Mentioned an open source project that provides known-secure container base images called "chain guard"
    - static analysis tools: "semgrep" and "sobelow"
    - dynamic testing: no solutions right now for elixir
    - runtime testing: https://paraxial.io/blog/exploit-guard
### Patterns
  - A couple of talks mentioned that returning values like `{:ok, data}` make it so you can't pipe the result somewhere else. `with` is a solution for this but it can end up hiding where errors come from if they're not unique enough. "Tokens" offered as a solution here (see "talks or articles mentioned" below)
  - Also monads seem relevant, but maybe controversial? There was a lighting talk about this which was interesting  https://tylerayoung.com/2024/08/29/lightning-talk-dont-say-the-m-word/ -- note this is a link to the code samples without context -- the talk walks through them
### Other random things that seem interesting
  - Flame is a lambda solution you can run on your own machines
  - Flow is a library for distributed processing of data, like for one-off jobs (not for continuous processing)
  - A few notes from a devops talk that was mostly about stuff we already do (speakers were the authors of "Engineering Elixir Applications")
    - environmental integrity: all environments are as identical as possible
      - e.g. use your .tool-versions file in CI/CD in docker image. Do this by parsing it into `steps.parse-asdf.outputs.elixir-version`
      - Use one file to define all application services
    - You can define github repository creation in terraform (kind of interesting, probably not worth doing for us)
    - create a reusable deployment script in bash (done) -- then run it on merge to main (continuous deployment)
  - José Valim made some interesting points in his keynote about client state including things like element focus, scroll position, and more. 
### Talks from this conference you might enjoy watching
  - "Phoenix Unplugged" Divya Sasidharan had nice slides and gave some introduction to metaprogramming in the context of Plug
  - "More testing, fewer tests" Tyler young, discussed above, pretty good introduction if you don't know about "parameterized," "property-based," or "snapshot" testing strategies.
  - "Rapid prototyping" Wojtek Mach goes through a lot of tooling tips, some of which was new to me.
  - José's Valim's keynote? He's a very charismatic and effective speaker but I'm not sure this topic was super relevant for us honestly. But interesting. If anyone watches it I'd be interested in talking about it.
### Other references worth checking out
  - Rich Hickey (author of Clojure) "Simple made Easy": https://www.youtube.com/watch?v=SxdOUGdseq4 was interesting, gives some insight into foundational perspectives in this community
  - René Föhring's talk about Tokens: https://www.youtube.com/watch?v=ycpNi701aCs
  - Accessing history in iex. This video wasn't mentioned but the technique was and this very short video is a nice demo: https://www.elixirstreams.com/tips/getting-previous-values-in-iex
### Sense of the Community
  - Folks at this conference were basically as we deduced: friendly and pretty homogeneous
  - This community is recognized as being friendly and they seem aware of that and try to live up to it.
  - It would be nice if there were more structured welcoming efforts, like we have in library conferences: newcomer dinners (or any organized dining), explicit welcomes from the podium, orientations to the community.
  - There's no conference backchannel, so the only way to ask questions or make a connection is to walk up to somebody.
### Community Directions
  - José's talk was about potentially bringing front-end developers to the elixir ecosystem by making it easier to write javascript front-ends for phoenix applications.
  - There may be a hope that the awesomeness of livebook compared to jupyter will lure data scientists over to elixir from python.
  - A point of pride for this community is that elixir makes it easy to open-source develop networked features that in other code ecosystems entire companies exist to develop, support, and sell.
