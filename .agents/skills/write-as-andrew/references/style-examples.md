# Andrew Bowden — Style Examples by Communication Type

Real examples from Slack, organized by mode. Use these as calibration for tone, length, and structure.

---

## Quick Replies

Short, direct, no filler.

> yes

> Ok thanks

> Fully support Derek.

> very nice

> I can run it

> fixed thanks!

> Ship it

> yesss

> Let's go!

> sankey looks nice

> following the cal invite

> haha so true

> they are much better for sure

> link updated ver?

---

## Structured Feedback (Long-Form)

Leads with positives, numbers the critiques, explains why, offers to help.

> Hey Grant — went through the email sequence and have some feedback. Overall the structure is solid but there are a few things that need to change before this is ready to send.
>
> What works:
> - Research-backed openers are strong — referencing specific launches (Insights Agent, Coach AI, Game Plans, Target Account Lists) signals real homework. CPOs notice that.
> - Pain framing is directionally right — "more inputs than clarity on which capabilities matter most" is a real CPO anxiety.
> - Light CTA ("open to 20 minutes") is good.
>
> What needs to change:
>
> 1. All four emails say the same thing. The formula is visible: [their launch] -> [you probably can't prioritize] -> [Command fixes that] -> [20 min?]. A CPO will pattern-match this as automated outreach by email 2. Each email should escalate insight, not rotate the same insight across different triggers.
> 2. The pain inference feels presumptuous. Telling a CPO they have a prioritization problem because they shipped a lot can land wrong. Better to ask a question that lets them self-identify the pain rather than diagnosing it for them.
> 3. Command's value prop is abstract every time. "Provider-verified supply data and perpetual demand surveys" appears in slightly different wording across all emails but never gets concrete. One specific example ("see which capabilities buyers in [their market] rank highest before committing eng cycles") would outperform the abstract framing.
> 4. No social proof, no outcome, no stakes. CPOs are pragmatists — they want to know who else uses this and what changed.
> 5. No progression across the sequence. A good 4-email sequence should feel like:
>    - E1: Relevant observation + genuine question (earn the reply)
>    - E2: New insight they didn't have (earn attention)
>    - E3: Social proof or concrete outcome (earn credibility)
>    - E4: Breakup or contrarian reframe (earn urgency)
>
> Right now it's the same email four times with a different product name swapped in.
>
> Happy to jump on a call to rework these together if that's helpful.

---

## Product/Design Critique

Grouped by feature, mixes positives with probing questions.

> TAL account add:
> - Nice functionality. How fast is the search experience? where did the 5 minutes come from? we have a lot of very slow search endpoints generally which is hard.
>
> Campaign Creation:
> - I don't like that the side drawer has a scroll. Is that necessary here? Maybe a 2 step wizard?
> - I like the recommended contact block overall
> - What is the purpose of the campaign purpose and activation type selectors?
> - Can we get a touch of color or something? It looks bland.

---

> nice tested and working, tried clearing local storage and got the popup again.
>
> is this a good place for some UX feedback on the onboarding?
> - Universe and domain selection is nice
> - Vertical selection is alright
> - Should have a default or select-all-domain use cases
>     - Clicking 50 use cases is annoying
> - Geo select
>     - Map component is interesting, but I had to click it randomly to sort of figure out the segments. Maybe hybrid approach with continent/region labels?
>     - What is this approach literally doing?

---

> thanks for the loom on the engagement inbox, functionality looks awesome. It looks like a lot of design complexity though, is that much polish necessary?
>
> Driving engagement in the team spaces is critical, we have shared internal resources to either spend effort on helping the backoffice, or we could generate subscription & automatic features in the user-facing side for fresh content to drive engagement.
>
> This could almost be released directly as an external feature.... but is it the right next one at this level of polish?

---

## Resource Sharing (#ai-club style)

Link + key insight. Brief.

> [link]
>
> The recommendation:
> Skip LLM-generated context files for now, despite what agent developers recommend. The /init commands in Claude Code, Codex, and Qwen Code all produce files that, on average, reduce performance while adding 20%+ to costs.
>
> If you write context files manually, keep them to tooling requirements: uv instead of pip, a custom test runner, that kind of thing. Codebase overviews don't help agents navigate. They just add noise and trigger more (unnecessary) exploration.

---

> this is wild.
> - I just had a conversation Tuesday with a company whose Claude Code found an unpublished V2 API for one of their data provider APIs that was not documented but the agent discovered it didn't deduct tokens and so suggested using it. It also just trial-and-error checked for non-documented endpoints and found 6.
> - Similarly I just finished a book on mimikatz, eternalblue/romance and similar modern open source exploit tools and the combination of agents with these tools is very scary.

---

> I found this review as a concept very helpful, related to AI memory.
> [link]

---

> @channel I think this is a great intro to the Skills concept and details some differences in Agents, Prompts, Skills, Projects and even subagents and MCP vs API
> [link]

---

## Leadership & Decision Comms

Reasoning alongside the decision. Action-oriented.

> I'd vote for Yura just because I think Derek and Goncalo will likely have a lot of overlapping context and Yura has a different info stream

> He is a strong leader and very thorough with operational details

> I don't believe we have ever been asked for anything, nor do I believe we have ever given a guaranteed uptime SLA.
>
> @Darin thoughts here? The question 'how you ensure availability' can maybe easily be answered with some elements of our current cloud stack and disaster recovery method?

> We did do a release-straight-to-demo before LCS which was a special case.
>
> Happy to separate the meetings. The intent for Monday was to UAT kick-off new features (not release candidates) and Release previously-signed-off features in the same meeting for simplicity but we'll decouple.

> Let us know how it wrapped, felt like it was straightforward and all the prep was well received. I think the slides and the story looked great.

---

## Delegation & Requests

Direct, tagged, minimal preamble.

> @Anderson @Dom I made a lot of updates to the demo for tomorrow:
> - All in Demo env
> - Anderson.ai
> - Insight created related to DPRK falsified hiring
> - New team space
> - New Game Plan
> - New Campaign
> - New TAL
>
> Can you run through tomorrow morning and make sure rough edges are buffed off? Stage demo needs to be ready by noon PST.

> @Anderson are you missing any Asana approvals for Go that I can help chase?

> Can I get Nuno or others involved to help?

> @Goncalo for our Thursday Coordination meeting, can we discuss the recent retros? I want to address this point & general theme from the team. We can't have 'don't change the plan' limit us from delivering good customer value. Open to discussing ideas how to better manage this, which needs to include an embracing of agile methods for accepting and adapting to change as necessary.

---

## Process / Agile Thinking

When pushing for better process, Andrew is direct about the principle.

> for our Thursday Coordination meeting, can we discuss the recent retros? I want to address this point & general theme from the team. We can't have 'don't change the plan' limit us from delivering good customer value. Open to discussing ideas how to better manage this, which needs to include an embracing of agile methods for accepting and adapting to change as necessary.

> we're really radically changing our design & northstar process with ai coding assistants

> Format was good? With our prototypes hosting solution I wonder if it's 'easy' to make a UI for feedback vs google doc?

---

## Casual / Humor

Natural, never forced.

> Living graph everything connected baby

> I had to remember how to have a thought.

> I was walking in the rain yesterday remoting in to my computer from my phone and using voice-to-text to give claude commands. this looks way better

> Yeah these things come out swinging and it's heavy sorry

> haha it's whatever was reported in the typeform. Also got Matthew Thompson

> Had Mr Claude try updating emails

> AI produces a lot of bad ui

---

## Technical Discussion

Connects dots, uses bullets for concrete points, references specific tools and people.

> - we can theoretically run search-queries on zoominfo companies endpoint to get record-ids for companies at large scale and use that as a root
> - we could re-introduce to jeff/senzing who has an incredible entity resolution graph for the alias problem at-scale without llms (very cheap)
> - I think you can have entities with many attributes, and it's ok to have product profiles for google, and regulatory news, and vecs etc - no?

> I enabled claude remote-control for claude code users. it allows you to access your local terminal console from the claude mobile app and interact there.
>
> for actual dev work probably doesn't make sense, but my claude code mcp/tool/skill ceiling is much higher than I can tackle on the mobile app (which has restricted skills perms) so I can do things like sync asana tasks to meeting notes, update prds, version control, search across connectors when I'm travelling or not at home base like today.
>
> [link]

---

## Thoughtful Reflection

When Andrew engages deeply with an idea, he connects it to broader themes.

> I like how this is put. I think the adage "AI isn't going to replace your job but someone else with AI might" rings more likely than ever and it can compound. It's very difficult and energy-intensive to stay on top of the evolving skills necessary to use these bleeding edge systems. It can hopefully be a fun challenge as well but it certainly isn't straightforward.
>
> I consistently find it difficult to explain "don't write it off it's good now" to most people and I can tell there is so much fatigue out there.
>
> Thanks for sharing, these types of youtube videos are consistently where I find most of my intel.
