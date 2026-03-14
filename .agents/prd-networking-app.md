# PRD: Liminal Networking App

**Status:** Draft — for team review and feedback
**Version:** 0.5
**Date:** March 14, 2026
**Author:** Andrew Bowden (CPO/CPTO)
**Source:** Networking App Jam + Travis/Andrew follow-up (March 13, 2026)
**Reviewers:** Travis Jarae, Jennie Berry, Filip Verley
**v0.5 Changes:** Incorporated findings from multi-agent critical review (strategy, market, research methodology, requirements, positioning). Major additions: revised competitive landscape, strengthened tollgate methodology, added research bias safeguards, added requirements gaps section, added exit criteria.

---

> This PRD captures the output of exploratory brainstorming and frames it as a structured investment proposal. The concept has strong directional alignment with Liminal's strategic goals. To move forward responsibly, this document proposes a tollgate model: each phase unlocks the next only when defined success criteria are met. **We are asking to fund discovery (Tollgates 1-3), not development.** Engineering investment is deferred until demand is validated.

---

## 1. Problem Statement

### The Network Creates Real Value for Members — But It's Manual and Invisible

Liminal's curated network is genuinely valuable to the people in it. Filip and Will's 12 manual introductions to Doug Ailey at Paravision resulted in 6 deals for Doug — the kind of outcome that makes a buyer's career easier and a vendor's growth possible. The network works because Liminal has spent years building trust density among buyers, investors, and analysts in identity, fraud, and cybersecurity.

But this value is delivered entirely through manual, ad hoc effort. Filip, Travis, and a handful of senior team members carry the relationship graph in their heads. Members like Doug benefit when someone at Liminal happens to think of the right connection at the right time. There is no systematic way for members to discover each other, surface shared interests, or act on peer proximity.

Beyond introductions, buyers want something more specific: a **confidential space to benchmark with peers.** Are you struggling with deepfakes? Are you paying 30 cents per document verification on step-up? Is your selfie verification taking users 20 seconds? Buyers want consortium and consensus intelligence from people in the same position — without being sold to. Today, they get fragments of this at LCS and in ad hoc conversations. There is no persistent, structured way to ask these questions and get peer-validated answers.

### Valuable Network and Interaction Data Goes Uncaptured

Every introduction, every expert call, every conference hallway conversation generates signal about who knows whom, what buyers care about, and how the market is moving. Today, almost none of this is captured. The network's relationship graph, interaction patterns, and peer intelligence exist only in fragmented form across email threads, Slack messages, and people's memories.

A product layer that facilitates and tracks network interactions would create a structured dataset of relationship signals, engagement patterns, and peer sentiment — data that is extremely valuable for Liminal's intelligence products, for members seeking peer connections, and for understanding how the identity/fraud/cyber market actually operates at the decision-maker level.

### The Membership Framing Limits Network Growth

Access to the Liminal network is currently bundled with "membership." People cannot experience the value of being in the Liminal network without paying, and the membership framing signals "vendor community" to buyers who are specifically trying to avoid vendors. Decoupling the network layer from the paid membership could expand who participates and strengthen Liminal's identity as a technology platform.

### Connections Go Cold Between Events

The LCS CEO Summit (~87 attendees, 40+ CEOs) creates high-density, high-trust moments. But those connections exist in a relational vacuum for the other 350 days per year. There is no lightweight mechanism for members to stay warm with peers, act on connections made at events, or surface new relevant connections as contexts change.

### Supporting Evidence

- Filip and Will introduced Doug Ailey to 12 companies — he closed 6 deals and called them "the best introductions I've ever had"
- LCS CEO Summit: ~87 attendees, 40+ CEOs — proves buyers value curated peer interaction
- Buyers consistently respond to Liminal research outreach because of existing relationship trust
- Network interaction data (who connects with whom, what topics drive engagement, which introductions convert) is currently uncaptured and represents a significant intelligence asset
- Realistic addressable pool: 3,000-6,000 qualified individuals globally (identity/fraud/cyber decision-makers at enterprise scale). A 200-500 member club captures the most valuable segment.
- No buyer-side community exists for the **specific** identity/fraud/cyber buyer persona (CPO/CSO/CEO) with Liminal's combination of vertical depth, trust density, and curated buyer-only focus. (Note: broader CISO communities exist — see Section 12 for competitive analysis.)

---

## 2. Lessons from Past Attempts — An Honest Assessment

Liminal has attempted community networking three times. Each failed. The networking app concept must confront these failures directly, not paper over them.

### The Flywheel Thesis Has Been Tested Before

LAN (Liminal Answer Network, 2022-2024) was built on a strategic thesis that is remarkably similar to what this networking app proposes:

**LAN's thesis:** Build a proprietary expert network → capture intelligence from expert conversations → feed that intelligence into the Link platform → make Link more valuable → attract more experts. The core business problem was reducing Liminal's reliance on expensive external expert networks (like GLG) by building an in-house network. It was monetized through consulting ($40K-$200K research reports).

**The networking app's thesis:** Build a curated member network → capture relationship and engagement data → feed that data into the intelligence platform → make the platform more valuable → attract more members.

These are the same structural flywheel. The execution is different, but the strategic bet is the same. This PRD must be precise about what is structurally different in execution this time — not just assert that LAN was "a different product."

### What Failed and Why

**LAN (2022-2024):** The expert network was monetized through consulting deliverables. Experts got paid per call; clients got reports. There was no peer-to-peer value exchange, no community layer, and no reason for anyone to "join" beyond transactional engagement. The fundamental failure was **value asymmetry**: Liminal extracted intelligence from experts and sold it to clients. Experts were the product, not the beneficiaries.

**Slack Working Groups:** Topic-based channels with sporadic, event-proximity engagement ("Are you going to IIW?") but no sustained participation. Without genuinely exclusive content, the channels went quiet.

**Community Manager Seeding (Diana):** Manufactured engagement prompts that community playbooks recommend. The audience ignored them. Travis's assessment: unless the content is real insider intelligence, manufactured prompts don't work for this audience.

### What Must Be Structurally Different This Time

The critical lesson across all three failures is the same: **value must flow to members first.** In LAN, value flowed from experts to Liminal to clients. In Slack, no value flowed at all. With Diana, the prompts offered no insider value worth responding to.

The networking app must invert this. Members must receive tangible value (warm introductions, peer benchmarking, insider intelligence, exclusive access) before Liminal captures any data benefit. If members ever perceive the network as a data collection mechanism for Liminal's commercial products, the extraction dynamic reasserts itself.

| Dimension | Past Attempts | Networking App (proposed) |
|-----------|--------------|--------------------------|
| Value direction | Liminal extracts from members | Members receive value first; Liminal benefits second |
| Core offering | Paid reports / passive channels / manufactured prompts | Curated peer club with proactive, insider-driven engagement |
| Engagement model | Pull-based / editorial | Proactive push + community-generated insider content + circles |
| Cold start | None | Seed with 100+ LCS attendees, LCS gate, engagement requirements |
| What drives engagement | Nothing that worked | Real insider intelligence only — not manufactured content |

**Key design principle:** Members must never feel like the product being offered out to sales contacts. If the networking app recreates the extraction dynamic — even accidentally — it will produce the same outcome as LAN.

---

## 3. Strategic Context

### Why This Matters to Liminal

Travis's framing: shifting Liminal toward a pure tech company identity requires pulling the community and networking layer out of the membership model. The network should become a standalone product that demonstrates the value of being associated with Liminal, rather than something gated behind payment.

The long-term flywheel: at scale, the Liminal network becomes the distribution layer for GTM campaigns, Command intelligence, LCS events, and research surveys. The network creates reach; the platform creates value; the intersection drives revenue.

**Important caveat:** The flywheel requires scale to generate meaningful data. A 200-person club produces thin data — a nice Rolodex, not a data asset. The flywheel is a Phase 3 hope, not a Phase 1 reality. The cap is 200-500 members; with 40% WAU, that's ~200 active users generating data. The flywheel only activates at the maximum end of the stated club size. Phase 1 must stand on its own value to members (warm intros, peer benchmarking, exclusive access) without depending on the data flywheel to justify the investment.

**Structural honesty:** Only 2 of the 5 claimed differences from LAN are genuinely structural: (1) value direction (members receive value first) and (2) data governance firewall. The other differences (engagement model, cold start, content approach) are execution choices that the LAN team could also have made. The PRD should not overstate the structural gap between these two bets.

### The "Data and Relationships" Thesis

Travis's framing: in a world of cheap applications and AI, the two things that hold durable value are **data and relationships.** AI won't replace trust-based human connections until agents make all buying/selling decisions — and even early agentic purchasing experiments show that's far from reliable today.

Andrew cited the Gartner Peer Community data directly to Travis: businesses engaged in Gartner's peer network spend 2x more on Gartner products. **[Source needed: this stat could not be publicly verified during review. Must be sourced from Gartner directly or labeled as anecdotal before using in investment discussions.]** If accurate, it validates community-as-moat positioning — but note the structural difference: Gartner layers community on a $6B research/advisory business. Liminal would be building community to create the moat, not leveraging an existing one.

### Why This, Why Now — and What We're Not Proposing

This initiative is **not on the Q1/Q2 roadmap** and we are not proposing to reprioritize. Current strategic priorities (enterprise account depth, agentic ROI, Buyer App) are unchanged.

What we are proposing:

| Phase | Investment | Engineering Required |
|-------|-----------|---------------------|
| Tollgates 1-2: Concept alignment + buyer interviews | Leadership time (4-6 weeks) | None |
| Tollgate 3: Concierge validation | Community manager time (~10-15 hrs/week for 6-8 weeks) | None |
| Tollgate 4+: Build decision | TBD — only if T1-3 pass | Yes — assessed at T4 |

We are asking to fund discovery, not development. If Tollgates 1-3 fail, we stop with minimal investment. If they pass, we make a build decision with validated demand, a clear sequencing plan relative to the Buyer App, and a financial model.

### Trust Asymmetry — The Elephant in the Room

Liminal is simultaneously the host of a buyer community AND a company that monetizes intelligence about this market. This creates a structural tension: if buyers contribute insider intelligence (benchmarking data, peer questions, engagement signals) and then see that intelligence reflected in Liminal's commercial products, trust collapses instantly.

**Data governance principle:** Networking app member data is firewalled from Command, GTM, and research products. No member engagement data, no individual responses, no relationship signals flow into commercial intelligence products without explicit, granular member consent. Community insights (e.g., aggregated poll results) may be published only in anonymized, aggregated form — and only within the community itself, not in external Liminal reports.

Gartner's Peer Community model works because the community is perceived as separate from the analyst reports that Gartner sells. Liminal must achieve the same separation.

### Relationship to Existing Products

| Product | Relationship to Networking App |
|---------|-------------------------------|
| Command | Long-term convergence; NOT a data pipeline from member activity |
| GTM / Vex | Firewalled — member data does not flow to campaign targeting |
| Buyer App | Convergence opportunity: shared identity layer, network builds buyer consortium |
| LCS Summit | The networking app extends LCS year-round; LCS gates app access |

### Networking App + Buyer App Convergence

These products converge but cannot be each other's flywheel when both are pre-launch. The convergence is a 12-18 month vision:

- **Network → Buyer App:** Community of verified buyers creates consortium performance data the Buyer App needs.
- **Buyer App → Network:** Benchmarking users have a natural reason to join the broader peer network.
- **Shared identity layer:** Both need verified buyer identity — build once, benefit both.

**Critical decision required at Tollgate 1 (not deferred):** Both products target the same persona (enterprise buyers), both need verified buyer identity, and both propose data flywheels. Running both during a "depth over breadth" strategy creates resource conflict — not just engineering, but leadership attention (Travis, Filip, Andrew). T1 must produce a clear priority decision: if both are going, what gets priority when they conflict? The sequencing decision is not "convergence opportunity" — it is a resource allocation decision.

---

## 4. Target Users

### Primary: Buyers
Enterprise decision-makers — CEOs, CSOs, CPOs, CISOs — at companies purchasing identity verification, fraud detection, or cybersecurity technology. Minimum bar: LCS Summit buyer threshold.

### Secondary: Investors
VCs and growth equity investors in identity, fraud, and cybersecurity.

### Secondary: Analysts
Independent and institutional analysts covering the identity/fraud/cyber space.

### Open Question: Vendor Inclusion

**Design principle:** members cannot feel like the product.

**Potential resolution — the "Spaces" model:** Travis suggested separate spaces for buyers, vendors, and investors — each with different incentives and controlled cross-space interaction. Buyers get confidential peer benchmarking. Vendors get partnership/distribution space. Cross-space connections happen through Liminal-mediated, incentive-aligned interactions. To be evaluated at Tollgate 1.

### User Personas

**Sarah — The Enterprise Buyer (Primary)**
CISO at a Fortune 500 financial institution. Evaluates 3-5 major technology decisions per year. Finds LinkedIn noisy and vendor-dominated. Wants: efficient access to trusted peer perspective, not another place to be sold to.
- **What she uses today:** Private text threads, Gartner analyst inquiry calls (employer pays), Evanta/Gartner CISO peer groups, CyberRisk Collaborative, GLG/AlphaSights for expert calls, conference networking
- **Honest "so what?":** Her problem is **time, not access.** She has 45 minutes/week of discretionary peer time, already spoken for. Giving her more access doesn't solve a time problem. The value prop must be *faster, better answers from verified peers* — not *more connections.*
- **Value prop strength: 5/10.** Introductions solve a real but infrequent problem. Peer benchmarking competes with Gartner Peer Community her employer already pays for. Differentiator is vertical specificity in identity/fraud.

**Marcus — The Active Investor (Secondary)**
Growth equity partner. Wants early signal on buyer category exploration. Would participate if it gives him buyer access he can't get elsewhere.
- **What he uses today:** GLG/AlphaSights ($1K-$3K/call, expensed easily), portfolio company networks, Gartner/Forrester, Tegus/Alphasense
- **Honest "so what?":** Strong pull for initial sign-up, weak pull for sustained engagement. Will take every introduction and give nothing back unless structurally incentivized. Investors as members risk creating the exact "being sold to" dynamic that repels buyers, just from a different angle.
- **Value prop strength: 6/10.** Near-zero switching cost to join; near-zero switching cost to leave.

**Priya — The Independent Analyst (Secondary)**
Publishes research on digital identity and fraud. Wants primary source access to practitioners at scale.
- **What she uses today:** Personal network, LinkedIn DMs (low response), conference networking, vendor PR "customer references"
- **Honest "so what?":** Straightforward win — curated directory of 200 CISOs who've pre-consented to engage is extremely valuable.
- **Value prop strength: 8/10.** But creates a value asymmetry risk: Priya extracts from the network the same way Liminal would. If Sarah realizes Priya gets free practitioner access she monetizes through research, the "I'm being used as a product" alarm triggers.

---

## 5. Product Concept

### Core Metaphor: Club, Not Social Network

Travis: **"It has to be a club, not a social network."** Clubs work at 200-500 people. A club has an owner (Liminal) who actively engages members. Members join for:

- **Ego:** You got invited. You're part of something exclusive. Special events and people others don't have access to.
- **Convenience:** Direct connections without the LinkedIn runaround.

The critical distinction from LinkedIn or CTD: **every member has been vetted by Liminal, and every connection is warm by default.**

(Note: CTD/ctd.ai is a $24/employee/month sales enablement tool for sellers — not a community. Not a competitor. Real comparables: Hampton ($8M ARR, 1,000 members), Gartner Peer Community (2x platform spending), Pavilion ($11M+ ARR). None serve the identity/fraud/cyber vertical.)

### The Facilitated Introduction — Core Value Proposition

The single most important interaction in the product. This is what must work on day one for a seed member to find value.

**Flow:**
1. Member browses directory or receives a proactive suggestion ("You and 3 members are heading to RSA — want an introduction to Sarah, who's evaluating the same KYC vendors you are?")
2. Member taps "Request Introduction"
3. Liminal reviews fit and context (human-mediated in MVP/concierge, automated later)
4. Liminal sends warm introduction to both parties with relevant context
5. Both accept → Liminal connects them (email or in-app)
6. Post-intro: both parties rate whether the introduction was valuable

**UX philosophy:** Push notification → tap → done. No forms, no friction. Just tap-tap.

### Liminal Circles

Interest-based groups organized around topics, events, or geographies. A community manager (eventually AI) posts temporal prompts:

- "Who's going to RSA next week?"
- "Who's interested in a Q3 New York executive meetup?"
- "What do you think about the proposed EID regulation?"

Members raise their hand via push notification. Circles can be persistent ("Identity Fraud Practitioners") or temporal ("RSA 2026 Attendees").

### Community-Generated Content Pipeline

The daily engagement hook should be **community-generated, not editorially produced.** Past failures (Diana's manufactured prompts) prove this audience ignores generic content. Only genuinely valuable insider intelligence drives response.

- **Seed initially:** Operational benchmarking questions buyers actually want answered:
  - "Are you struggling with deepfakes in your onboarding flow?"
  - "What are you paying per document verification on step-up?"
  - "Is your selfie verification taking users more than 15 seconds?"
- **Community takes over:** Aggregated peer sentiment ("Here's how 47 CISOs answered this week's question") becomes the insight.
- **Engagement as connection catalyst:** "You and 3 members near San Francisco all flagged document fraud — want an introduction?"

### Anonymous Posting — The "Rumor Circle" (Phase 2)

Travis's strongest engagement signal: "I'm all about trying to get rumors in the platform." Anonymous posting lowers the barrier to sharing sensitive market intelligence.

**Deferred to Phase 2** for three reasons:
1. **Trust must exist before anonymity is safe.** In a 30-50 person network, anonymous posts are pattern-matchable to likely authors. This could damage trust in the early critical period.
2. **Legal exposure.** M&A rumors, competitive intelligence, and pricing data from Fortune 500 executives create potential liability. Legal review required before implementation.
3. **Not needed to validate the core thesis.** Warm intros + circles validate engagement. Anonymous posting is an engagement enhancer for a network that already works.

### LCS as Enrollment Gate

Travis: **"If you're not on this app, you don't get invited to the summit."** Making the networking app the gateway to LCS creates an immediate, high-value reason to join.

### Engagement Requirements

Travis noted Hampton requires minimum engagements per month/quarter — "the only way to actually do it" for overcoming cold start. Combined with the LCS gate, this creates a two-sided retention mechanism. Specific thresholds to be defined and tested during Tollgate 3.

---

## 6. Platform Approach

### Web App First, Mobile Long-Term

**MVP:** Responsive PWA with push notification support. Lower engineering lift, faster iteration.

**Phase 2+:** Native iOS (priority) and Android if web app validates. Native unlocks richer location services and background notifications.

---

## 7. Investment Tollgates

Each phase unlocks the next only when defined criteria are met.

### Tollgate 1: Concept Alignment (2-4 weeks)

**Objective:** Shared product definition across leadership.

**Required outputs:**
- Vendor policy decided (Travis + Filip)
- Communication governance model defined
- Monetization direction (free community-as-moat vs. premium tier) — this cannot remain ambiguous past T1. Free = cost center justified by indirect revenue (must define measurement). Paid = must define what justifies $2-4K/year.
- **Buyer App resource priority decision** — not a convergence plan, but: if both are going, what gets priority when they conflict? This is a resource allocation decision for leadership attention, not just engineering.
- Vetting criteria beyond "LCS threshold"
- **Legal review initiated** — GDPR/CCPA applicability, Terms of Service, content liability for named member posts, data governance compliance. Legal review is the longest-lead dependency; it must start at T1, not wait for T4.

**Gate:** Documented decisions on all six items within 4 weeks. If alignment cannot be reached, pause.

### Tollgate 2: Demand Validation (3-4 weeks, parallel with T1)

**Objective:** Test whether buyers will commit to participating, not just express polite interest.

**Method:** 10-15 structured interviews with recent LCS buyers.

**Gate:** 8+ of 10+ buyers **commit to participating** in a 6-week concierge trial with their real identity and at least 2 hours of engagement. (Not "express interest" — behavioral commitment.)

### Tollgate 3: Concierge Validation (6-8 weeks)

**Objective:** Test the engagement model with real people, zero engineering investment.

**Method:** Liminal team manually operates the networking experience for 30-50 seed members from LCS (Travis confirmed 100+ would join — strong seed pool).

**Gate criteria (measured in final 2 weeks of concierge, not first 2 weeks):**
- 60%+ of members complete 2+ explicit engagements (introduction acceptance, circle hand-raise, or content response) in the final 2 weeks
- NPS 45+ from participating members (white-glove concierge with trusted seed members should earn premium scores)
- 5+ completed introductions where the recipient reports the connection was useful in a 1-week follow-up

**Pre-T3 requirements:** Introduction flow protocol defined, engagement tracking method in place, and community manager assigned.

### Tollgate 4: MVP Build Decision

**Objective:** Commit engineering resources based on validated demand.

**Required outputs:**
- Financial model: build cost, operating cost, expected return (direct or indirect)
- Capacity assessment and trade-off analysis vs. Buyer App and Q3 priorities
- Technical architecture decision (PWA, shared identity layer)
- Sequencing decision: networking app parallel or sequential with Buyer App
- Legal review of Phase 2 anonymous posting model
- MVP scope finalized based on concierge learnings

**Gate:** Executive approval of investment and trade-offs.

### Tollgate 5: MVP Launch Metrics (60-90 days post-launch)

| Metric | Target | Priority |
|--------|--------|----------|
| Member acceptance rate | 50%+ | |
| Weekly active rate | 40%+ | P0 — must pass |
| Connection request rate | 15%+ | |
| Intro completion rate | 40%+ | P0 — must pass |
| Community content engagement | 25%+ | |

**Gate:** Both P0 metrics must pass. Hit 3+ of the remaining 3 targets. If fewer than 2 of 5 total, evaluate whether to iterate or sunset.

---

## 8. MVP Scope (Post-Tollgate 4)

### In Scope (Hard Core)
- **Curated member directory** — Searchable, filtered by role, industry, geography
- **Facilitated introduction flow** — The core value prop: request intro → Liminal reviews → warm connection → rating
- **Liminal Circles** — Event-based and topic-based hand-raise groups with temporal prompts
- **Community-generated content** — Polls/questions with aggregated peer insights, seeded by Liminal
- **Proactive notifications** — Push notification → tap → done UX
- **Invite-only onboarding** — Manual vetting gate, minimal profile
- **Responsive web app (PWA)**

### Out of Scope for MVP
- Anonymous posting / rumor circle (Phase 2 — requires trust foundation + legal review)
- Direct messaging (Phase 2 — requires communication governance from T1)
- Vendor profiles
- Self-serve signup
- Command/GTM/Scout integration
- Native mobile apps
- Paid membership

### Phase 2 (unlocked at Tollgate 5)
- Anonymous posting with moderation infrastructure and legal-reviewed content policy
- Controlled direct messaging with guardrails
- Concierge experience (personalized event briefings, strategic intro recommendations)
- Native iOS app
- LCS event calendar integration
- Light Command integration (connection suggestions informed by market intelligence)

### Phase 3: Flywheel Activation
- GTM integration (with explicit member consent)
- Buyer App integration (consortium performance data)
- AI-powered community management
- Research survey distribution via network
- Self-serve member referrals with approval
- Android support

---

## 9. Risks and Mitigations

### Risk 1: Cold Start — The Pattern of Past Failures
Three prior attempts failed at sustained engagement. Clubhouse lost ~70% of MAUs; Lunchclub raised $56M and stagnated.
**Mitigation:** Seed with 100+ LCS attendees who already trust each other. LCS gate + engagement requirements create retention. Community-generated insider content (not manufactured prompts) drives quality. Concierge phase (T3) tests this before engineering investment. Critically: measure engagement in the final 2 weeks, not the first 2 — novelty decays.

### Risk 2: Value Asymmetry — The LAN Pattern
The same flywheel thesis failed with LAN because Liminal extracted value from the network without proportional return. The networking app has the same structural risk: members contribute insider intelligence and Liminal captures the data.
**Mitigation:** Data governance firewall (Section 3). Value must visibly flow to members first. No member data in commercial products without explicit consent. Design review at every phase: "Can we articulate the member value of this feature without referencing Liminal's commercial benefit?"

### Risk 3: Trust Asymmetry
Liminal hosts the community AND monetizes market intelligence. Buyers at this level are sophisticated about data usage.
**Mitigation:** Explicit data governance architecture (Section 3). Networking app data is siloed from Command/GTM. Aggregated insights stay within the community. Gartner separation model: the community is perceived as distinct from the commercial intelligence products.

### Risk 4: GTM Cannibalization
**Mitigation:** MVP uses facilitated introductions, not direct messaging. Communication governance defined at T1.

### Risk 5: Vetting at Scale
Chief scaled to 20K and collapsed. Soho House to 185K at depressed valuation.
**Mitigation:** Hard cap (200-500, never exceed 1,000 without tollgate review). Increase selectivity over time (Hampton model).

### Risk 6: Engineering Capacity
**Mitigation:** Tollgate model defers engineering until T1-3 pass. Web app reduces scope. Financial model required at T4.

### Risk 7: Digital-Only Engagement Decay
**Mitigation:** App augments in-person connections (LCS, dinners, RSA meetups), doesn't replace them. Hybrid > digital-only.

### Risk 8: Anonymous Content Legal Exposure (Phase 2)
M&A rumors, competitive intelligence, and pricing data from Fortune 500 executives create potential liability for the hosting platform.
**Mitigation:** Anonymous posting deferred to Phase 2. Legal review required before implementation (flagged as T4 output). Content moderation policy and infrastructure must be in place before launch.

---

## 10. What's Validated vs. What We Need to Learn

### Validated
- Warm intros convert (12 intros → 6 deals for Doug)
- Buyers value curated peer interaction (LCS: 87 attendees, 40+ CEOs)
- Buyers respond to Liminal outreach because of existing trust
- The flywheel thesis (network → intelligence → platform) was strategically sound in LAN — execution (extraction > contribution) was the failure
- Manufactured community prompts don't work — only real insider intelligence drives engagement

### Needs Validation (Tollgate 2)
- Buyers will commit (not just express interest) to active participation in a digital peer network
- Community-generated content (peer benchmarking questions, aggregated insights) is a sufficient engagement driver
- The "club not social network" framing resonates with target members

### Needs Validation (Tollgate 3)
- Sustained engagement beyond novelty (measured in final 2 weeks, not first 2)
- Members contribute content, not just consume
- Facilitated introductions are perceived as valuable enough to drive repeat engagement
- 30-50 members is sufficient density for a useful experience

### Longer-Term Hypotheses (Phase 3)
- The data flywheel materializes at scale (requires 500+ active members)
- The networking app improves Liminal's positioning as a tech platform
- The networking app and Buyer App converge into a unified buyer ecosystem

---

## 11. Open Questions for Tollgate 1

| # | Question | Owner |
|---|----------|-------|
| 1 | Vendors in or out? Evaluate the "spaces" model | Travis + Filip |
| 2 | Communication governance for member-to-member interaction? | Travis + Jennie + Andrew |
| 3 | Free community-as-moat, or eventual paid tier? | Travis |
| 4 | Networking app + Buyer App: parallel or sequential? Shared identity layer? | Andrew + Travis |
| 5 | Explicit vetting criteria beyond "LCS threshold"? | Filip + Travis |
| 6 | Who is the community manager for Tollgate 3? | Andrew |

---

## 12. Competitive Landscape

(See Notion page for full competitive analysis with detailed comparables, success patterns, failure modes, and pricing benchmarks.)

**Strategic positioning:** Community-as-moat, not community-as-product. Closest analog: Gartner Peer Community (2x spending from engaged members). Closest operational model: Hampton (1,000 members, $8M ARR, 8% acceptance rate). Vertical white space: no buyer-side community exists in identity/fraud/cybersecurity.

---

## Appendix: Meeting Context

### Source 1: Networking App Jam (March 13, 2026)
**Attendees:** Travis Jarae, Filip Verley, Andrew Bowden, Jennie Berry, + 2 others
**Key framing:** Travis — shift to tech company identity, decouple network from membership. Filip — "subliminal in your pocket," proactive nudges, no vendors. Andrew — LAN was consulting, not community; cold start was the core issue.

### Source 2: Travis + Andrew Follow-Up (March 13, 2026)
**Key framing:** Travis — "club not social network," ego + convenience, data and relationships are durable, spaces model, engagement requirements (Hampton), loves rumors in the platform, confirmed 100+ from LCS would join. Andrew — buyer peer benchmarking, Gartner 2x stat, network data as moat, concierge model (Travis: "step two"), Liminal Circles, anonymous posting, tap-tap UX.

### Source 3: Andrew — Additional LAN Context
LAN's core business problem was reducing costs of external expert networks (GLG). Monetized through consulting. Fundamental belief: own expert network would be the force behind Link → full flywheel. This is the same strategic thesis as the networking app, with different execution.

---

*The tollgate model allows the team to invest incrementally — no large commitment is needed until the concept proves itself through validated demand.*
