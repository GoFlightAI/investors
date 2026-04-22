# GoFlight Brief — April 22, 2026
## For Claude Code & Project Sessions

---

## BUSINESS CONTEXT

**Company:** GoFlight.ai — charter operations platform for mid-size US operators (10–30 aircraft)  
**Stage:** Pre-revenue, thesis locked, design partner pursuit active  
**Burn Rate:** ~$500–700/mo (AWS ~$350, GitHub $8, M365 $30, Hetzner TBD)  
**Runway:** ~12 months at current burn (day job funds operations)  
**Business Model:** Usage-based pricing to operators and brokers. Pricing unit and tier structure under active discussion — will be tested with first design partner before finalization. Break-even economics acceptable Year 1; goal is proof-of-traction and data foundation, not margin.  
**Capital Strategy:** Not raising venture capital. Considering angel capital in 60–90 days if design partner signed and memo tested externally. Company run to preserve bootstrapping optionality.

**Founder:** Jack Bradham — sole founder, 100% owner  
**Corporate Entity:** Delaware C-Corp, 100% owned by Jack Bradham  
**Advisors:** Murat (formal advisor, being onboarded), Lazo Qaradaxi (industry advisor, no equity), Aaron Fiser (industry sounding board, not a buyer)

---

## THE THESIS

**Elevator:**
> *Don't buy software. Flyn does the busywork. You help customers, fly planes, and make deposits.*

**Executive:**
> *Flyn will increase revenue and elevate the experience of everyone in your operations by taking care of the busywork — chasing vendors, propagating changes, tracking trips — freeing your team to focus on customer experience and booking deposits.*

**What GoFlight IS:** A charter operations platform for 10-to-30-aircraft US owner-operators who run their own booking, manage their own trips, and are drowning in coordination work their existing tools can't do.

**What GoFlight IS NOT:** A marketplace, a quoting engine, or an Avinode replacement. GoFlight lives in the workflow that happens *after* the quote is accepted.

**The agent is named Flyn.** Flyn is an always-on teammate that absorbs coordination work: chasing vendors, tracking trips, propagating changes, collecting documents, flagging what's missing. Flyn doesn't replace the dispatcher's relationships or the owner's judgment. Flyn takes the time back.

---

## WHY THE CATEGORY IS BROKEN

The tools exist. Avinode, FL3XX, and the enterprise platforms do quoting, fleet visibility, and compliance reporting well. What they don't do is the coordination work itself. Their seat-license pricing is also out of reach for most broker-operators.

The dispatcher still chases the caterer manually. The owner-operator still updates the FBO by text. The trip state still lives in her head, a spreadsheet, and a WhatsApp thread with the crew. The category spent a decade building control panels for a job that needed a colleague. A dashboard can show you the work. It cannot do it. Until recently, that was true of any software.

---

## PRODUCT STATUS

### Live Platform
- Operator onboarding wizard
- Trust score system (history 30%, response 30%, completion 40%; new operators default 0.5)
- Chat/messaging core
- Flyn AI assistant (basic — formerly Wingman, renamed to Flyn)
- Operator vetting Lambda microservice
- Mobile-responsive UI
- ARGUS/Wyvern safety badges + Part 135 compliance display
- Stripe payments live

### Critical Build Path (Pre-Design-Partner)
1. **Flyn coordination features** — vendor follow-up, change propagation, trip tracking, document collection
2. **Demo path** — narrow slice of owner-operator operations flow showable on an iPad at a bar
3. **Anonymous Flyn conversations** (allow unregistered users to interact)
4. **Confirmation flow** (verify booking details before submission)
5. **Session history** for Flyn interactions

### Feature Freeze
New feature work is frozen through May 18. All effort concentrated on paring existing platform to the owner-operator demo path.

### Known Bugs (Pre-Launch)
- Chat scrolling issues
- Notification dropping
- User management errors
- Operator approvals API failures (intermittent)

### Testing Status
- **CRITICAL:** No end-to-end user test completed
- Success criterion: 1 real person completes a booking via Flyn with a real or test operator
- No load testing at scale

---

## TECHNICAL ARCHITECTURE

### Stack
- **Frontend:** React (responsive, Bauhaus design + warm copy)
- **Backend:** Lambda microservices per domain (operator_vetting, pricing, messaging, etc.)
- **API Gateway:** Per-service endpoints (NOT unified api.goflight.ai)
- **Database:** DynamoDB (goflight-tasks, goflight-event-log)
- **CI/CD:** GitHub Actions → straight-to-main (no PRs, no feature branches)
- **Deployment:** CloudFront + S3 (frontend); Lambda (backend)
- **Infrastructure:** Hetzner CPX31 (16GB RAM, 4GB swap) for supporting services
- **AI:** Model-agnostic — DeepSeek V3, GPT-4.1, Gemini 2.5, Claude (always best + cheapest); crons on Gemma4 (zero Anthropic spend on automation)

### Current Issues
1. **Per-service API Gateway** instead of unified endpoint (scalability debt)
2. **SPEC.md scope bloated** — needs full rewrite for current reality (cancellation tiers, AI moderation logic, operator vetting incomplete)
3. **Pricing rules undefined** — will be tested with design partner
4. **Documentation gaps** — cargo integration, empty legs matching, payment flow all undefined

---

## COMPETITIVE LANDSCAPE

Three groups matter. None is fatal; together they define where GoFlight plays.

### Avinode and the Quoting Marketplaces (COMPLEMENTARY)
- Entrenched, profitable, 20+ year incumbent (owned by CAMP Systems)
- ~3,400+ aircraft, seat-license pricing (~$1,500+/month starter tier)
- Moat: operator inventory and network relationships
- **GoFlight's relationship:** Complementary, not competitive. Operators continue using Avinode for sourcing; GoFlight lives in the workflow after the quote is accepted.

### Hamilton AI (CLOSEST PEER)
- Raised: ~$9.8M (seed $7.5M Mar 2026 + pre-seed)
- Status: Shipping since 2024, embedded banking (Column partnership Apr 2026)
- Intake: email, WhatsApp, Avinode, Airmail — NO voice
- **Prediction:** VC-scale economics will concentrate Hamilton on enterprise operators (50+ aircraft). Mid-market 10-30 is harder to serve profitably at their cost structure. That's where GoFlight starts.
- **GoFlight's edge:** Voice AI (live at +1 305-363-1121), model-agnostic stack, $20/mo self-serve vs. enterprise sales cycle, SMB focus

### Enterprise Charter Management (FL3XX, Portside, similar)
- Powerful, expensive, configured for operators with dedicated IT
- Sell dashboards, not colleagues
- Their buyers tend to be larger than GoFlight's beachhead
- GoFlight's buyers look at these tools, balk at price and complexity, return to WhatsApp

---

## TARGET CUSTOMERS

### Beachhead (First 90 Days)
US owner-operators running 10–30 aircraft who do their own charter booking in-house. Both sides of the transaction (inventory + demand) in the same building. Fastest feedback loops, single decision-maker, highest concentration of the pain GoFlight solves.

**Market size:** ~3,000–4,000 Part 135 certificate holders operating ~11,000+ aircraft nationally. Beachhead is the 10–30 aircraft mid-market within this population.

### Expansion (Months 4–12)
Independent charter brokers who work with those operators. Same logistical pain, come in through existing operator relationships (no cold acquisition).

### Not a Target (Yet)
Enterprise operators with 50+ aircraft and dedicated IT teams. Their procurement cycles, integration demands, and security reviews are not a fit for GoFlight's stage.

---

## GO-TO-MARKET STATUS

### Strategy: Design Partner First
The primary GTM motion for the next 30–60 days is signing one design partner — an owner-operator in the 10–30 aircraft range willing to use an early version of the tool, give weekly feedback, and be quoted publicly when happy. Everything else (events, content, scaling) comes after.

### Warm Contacts

**Aaron Fiser**
- Status: Industry sounding board, not a buyer
- Role: Discovery call target, ICP/messaging input
- Next: Structured call, recorded, synthesized

**Lazo Qaradaxi**
- Status: Industry advisor (no equity), warm lead from NBAA Cleveland (Mar 24–26)
- Next: Re-engagement for operator introductions

**Bryce Cannon (Vantage Air)**
- Status: Pinged Mar 22, slow response
- Email: Bcanon@vantageair.com
- Next: Re-engage or deprioritize

**Bill McBane**
- Status: Potential introduction source for FBO network
- Next: Ask for 3–5 FBO operator intros

### Trade Shows
- NBAA SDC Cleveland (Mar 24–26) — attended, pitch was NOT market-ready
- NBAA White Plains (May 20) — **CONDITIONAL:** attend only if design partner closable in person or marketing-ready artifact exists
- NBAA-BACE October 2026 — target (25K attendees, critical for scaling)

### Messaging (Locked)
- **Core:** "Tell us what you need. We handle the rest."
- **Subline:** "We're making charter aviation much easier. One conversation at a time."
- **What You DON'T Sell:** AI, cheap flights, or technology
- **What You DO Sell:** Time back, coordination relief, operator liberation
- **Voice:** Direct, punchy, human, confident (not arrogant), playful. No jargon.
- **Feel:** Warm, honest, easy, approachable, reliable, disruptive

---

## PHASE PLAN

### Phase 1 (Now — Months 0–9): Operations Platform for Owner-Operators
Win the daily workflow of 10–30 aircraft US operators. Earn the right to be their system of record. All product and GTM effort concentrated here.

### Phase 2 (Months 9–18): Expansion into Brokers
Same platform opens brokered workflow to independent charter brokers. Come in through operator relationships. Product surface expands modestly; GTM expands meaningfully.

### Phase 3 (18+ Months): Transparent Marketplace Built on Operations Data
Completed trip data flowing through GoFlight becomes structurally richer than any quoting marketplace has ever had. That data unlocks a customer-facing front door, transparent pricing, and a marketplace that competes on truth. The marketplace is earned by the operations layer, not built in parallel to it.

---

## NEXT 30 DAYS (By May 18, 2026)

1. **One-sentence pitch refined in public** — said out loud 20+ times, iterated from real reactions
2. **Three discovery calls completed** with owner-operators in the 10–30 aircraft range (including Aaron Fiser). Structured, recorded, synthesized into ICP and messaging.
3. **One design partner signed** (handshake) — using early tool starting in June, willing to give weekly feedback, willing to be quoted publicly
4. **Demo path built and shipping** — narrow slice of owner-operator ops flow showable on an iPad at a bar
5. **Revenue model documented** — pricing unit, target price point, first-year unit economics on napkin math
6. **One advisor formalized** (Murat) and one founder peer community joined
7. **Updated external-ready strategy memo** with design partner named
8. **NBAA White Plains decision** (May 20): attend only if design partner closable in person

---

## CRITICAL DECISIONS NEEDED

### By May 18
1. **Design partner commitment** — Who is it? Signed or not?
2. **Pricing unit decision** — What's the pricing unit for usage-based model? Tested with partner?
3. **NBAA White Plains** — Go or no-go?
4. **Demo path scope** — What's the minimum slice that tells the story on an iPad?

### By June 30
1. **Design partner actively using product** — Weekly feedback loop running
2. **End-to-end user test** — 1 person completes booking via Flyn
3. **Revenue model validated** — Pricing unit tested, unit economics documented
4. **Angel capital decision** — Raise or continue bootstrapping?

### By October 2026
1. **NBAA-BACE strategy** — Booth? Speaking slot? Demo-ready product?
2. **Multiple operators onboarded** — Booking volume trending
3. **Broker expansion readiness** — Phase 2 product surface scoped

---

## FOUNDER

**Jack Bradham** — sole founder, 100% owner, Delaware C-Corp.

Senior Solutions Architect at Amazon Web Services (third year), with prior time at Microsoft and Google Cloud — roughly 15 years across the three major cloud providers. Specialties: GenAI, cloud architecture, data analytics. Day job pays the bills and subsidizes the current stage of GoFlight — no personal savings burn, no pressure to raise before ready.

Deep in the Anthropic developer ecosystem: runs his own AI gateway and a production agentic coding workflow. Technical credibility to build agent-native software is present. The work of the next 90 days is primarily customer discovery, positioning discipline, and organizing around one lane.

**Team need:** One formal advisor (Murat, in progress), a founder peer community, and in 45–60 days fractional GTM help or an aviation-industry seller on aggressive commission.

---

## RUNWAY & FINANCIAL CONSTRAINTS

**Monthly Burn:** $500–700  
**Runway:** ~12 months (assumes no hiring, no infrastructure scaling)  
**AI Costs:** Pay-as-you-go; crons on Gemma4 (zero Anthropic cost)  
**AWS:** ~$350/mo (compute, storage, data transfer)

**Timeline:**
- **Now:** $0 revenue
- **6 months (Oct 2026):** Must have 1+ operators live, booking volume trending
- **12 months (Apr 2027):** Meaningful traction or reassess

---

## KNOWN UNKNOWNS

1. **Hetzner cost** — Needed for exact burn rate calculation
2. **Pricing unit** — Usage-based, but what unit? Per trip? Per seat? Per action? Testing with design partner.
3. **Operator vetting logic** — Trust score formula; parallel onboarding capacity?
4. **Cancellation tiers** — Refund policy for operator/customer cancellation undefined
5. **AI moderation** — Rules for flagging unsafe flights undefined
6. **Empty legs matching** — Algorithm undefined (Phase 2+ feature)
7. **Cargo integration** — Separate workflow path undefined (Phase 2+ feature)
8. **Payment flow** — Wire/ACH integration for operator payouts beyond Stripe cards

---

## KEY CONTACTS

**Business:**
- Jack Bradham: jack@goflight.ai (M365), jackb@live.com (Outlook), hello@goflight.ai (general)
- Murat: formal advisor (being onboarded)
- Lazo Qaradaxi: industry advisor, no equity (NBAA Cleveland lead)
- Aaron Fiser: industry sounding board (discovery call target)
- Bryce Cannon (Vantage Air): Bcanon@vantageair.com
- Bill McBane: FBO intro source

**Competitors:**
- Hamilton AI: Wouter Witvoet (wouter@hamilton.ai, 302-563-3823) — $9.8M raised
- Avinode: incumbent, complementary (not direct competitor)
- FL3XX / Portside: enterprise tools, not our segment

**CPA:**
- Kermit Bolick (Huggins CPA): kkbolick@hugginscpa.com

---

## REFERENCE DOCS

- **Strategy Memo v3:** GoFlight_Strategy_Memo_v3.docx (canonical positioning document)
- **Pitch Deck v3:** GoFlight_Pitch_Deck_v3.pptx (12 slides, matches strategy memo)
- **Investor Site:** GoFlight_Investor_Site.html (password-gated, matches v3 positioning)
- **Business Plan:** GoFlight_Business_Plan.docx (updated to reflect v3 pivot)
- **Operating Costs:** GoFlight_Operating_Costs.xlsx (needs refresh)

---

## THE HONEST TRUTH

GoFlight is a platform with significant existing infrastructure that is being pared ruthlessly to the owner-operator demo path. The thesis is locked after pressure-testing with Murat and against the competitive landscape. The positioning pivoted meaningfully in April 2026: from marketplace to operations platform, from Wingman to Flyn, from broad charter to 10–30 aircraft owner-operators, from competing with Avinode to complementing it.

The next 30 days are not primarily technical. They are: customer discovery (3 calls), pitch refinement (20+ reps), design partner signed (1 handshake), and demo path shipping. If those happen by May 18, GoFlight has earned the right to attend White Plains, consider angel capital, and expand.

If they don't, the thesis needs another turn.

---

**Document updated:** April 22, 2026  
**For:** Claude Code sessions, project briefings, advisor/partner discussions
