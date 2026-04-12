# GoFlight Brief — April 10, 2026
## For Claude Code & Project Sessions

---

## BUSINESS CONTEXT

**Company:** GoFlight.ai — operator-first charter marketplace  
**Stage:** Post-soft-launch, zero revenue, zero paying customers  
**Burn Rate:** ~$500-700/mo (AWS ~$350, GitHub $8, M365 $30, Hetzner TBD)  
**Runway:** ~12 months at current burn  
**Business Model:** 3% flat transaction fee + future SaaS upsell ($99-299/mo for premium tools)  
**Exit Target:** $300-400K revenue (Strukt&Proto insurance + income)  

**Owner:** Jack Bradham (solo GTM after Adam's departure)  
**Co-Founder Status:** Adam Hensley departing; minimal contribution to date

---

## PRODUCT STATUS

### Live Features
- Operator onboarding wizard
- Trust score system (history 30%, response 30%, completion 40%; new operators default 0.5)
- Chat/messaging core
- Wingman AI assistant (basic)
- Operator vetting Lambda microservice
- Mobile-responsive UI
- ARGUS/Wyvern safety badges + Part 135 compliance display

### NOT BUILT (Critical Gap)
1. **Wingman Features (5 specs drafted, 0 built)**
   - W-003b: Anonymous Wingman
   - W-003c: Confirmation flow
   - W-006: Omnichannel
   - W-007: Channel switching
   - W-008: Wingman-first landing
2. **Wingman session history** (P1 priority)
3. **Live deals carousel** in Wingman panel
4. **Conversation carousels** in Wingman panel
5. **Pricing engine** (CRITICAL: Tivoli launches May 2026)
6. **Empty legs module** (speed to market advantage)
7. **Cargo module** (identified as top revenue source)

### Known Bugs (Pre-Launch)
- Chat scrolling issues
- Notification dropping
- User management errors
- Operator approvals API failures (intermittent)

### Missing Documentation
- SPEC.md outdated (cancellation tiers, AI moderation logic, operator vetting incomplete)
- Pricing rules undefined
- Cargo integration path undefined
- Empty legs matching algorithm undefined

### Testing Status
- 10 items in testing queue
- **CRITICAL:** No end-to-end user test completed (1 real person booking via Wingman = success criterion)
- No real operator or customer validation
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
- **Agents:** All crons on Gemma4 (free/local); zero Anthropic spend on automation

### Current Issues
1. **Pipeline DOWN** (Apr 7) — blocks Gremlin QA, Audit spec compliance, task verification
2. **Per-service API Gateway** instead of unified endpoint (scalability debt)
3. **Agent infrastructure fragile** — scope too large, unclear role boundaries
4. **SPEC.md scope bloated** — needs full rewrite for current reality

### Nerd Board
- `nerds.struktproto.com` — Task Board + Factory Output (live)
- API Gateway: nmv5m59txi
- Lambda: nerd-board-api
- S3: nerds-struktproto
- CloudFront: EOCRVREOKTJFB
- Task DB CLI: `python3 ~/.openclaw/skills/dev-workflow/scripts/task-db.py`
- State machine: TODO → IN_PROGRESS → TESTING → VERIFIED → DONE (enforced)

---

## COMPETITIVE LANDSCAPE

### Direct Competitors

**Hamilton AI**
- Raised: $10M
- Status: Live, auto-quote engine active
- Strength: Speed-to-quote, $10M runway
- Weakness: Email-only workflow
- Founder: Wouter Witvoet (wouter@hamilton.ai, 302-563-3823)

**Tivoli**
- Raised: ~$50M (est)
- Status: Growing; 4K operators, 3M txns/yr
- Strength: Operator scale, established relationships
- Weakness: Email-centric (like Hamilton), operator→broker flow (not direct)
- Launch: AI pricing engine May 2026 (CRITICAL TIMELINE)

**Others (Mature/Struggling)**
- Avinode: B2B only, no direct-to-consumer
- XO/Vista: Expensive membership model
- FlyHouse: Reverse auction app model
- Villiers: Broker-only
- Wheels Up: Struggling

### Your Edge
1. Speed to market (if pipeline fixed)
2. AI UX (Wingman positioning as demand intelligence, not calendar mgmt)
3. Operator economics (3% flat fee, no hidden markups)
4. Transparency (3% breakdown, no monthly fees)
5. Direct operator-to-passenger (no broker middleman)

### Window
- **6 weeks** before Tivoli prices (May 2026)
- **6 months** before Hamilton scales deeper
- **6 months** to prove operator model works

---

## GO-TO-MARKET STATUS

### Framework (Planned, Not Executed)
1. Operator acquisition
2. Demand generation (content, SEO)
3. Scaling

### Warm Operator Contacts (Actionable)

**Bryce Cannon (Vantage Air)**
- Status: Pinged Mar 22, took 12 days to respond
- Email: Bcanon@vantageair.com
- Next: Confirm conversion timeline or pivot to Lazo

**Lazo Qaradaxi**
- Status: High-priority warm lead from NBAA Cleveland (Mar 24-26)
- Next: First call by Apr 15 (if Bryce stalls)

**Jacob (Switzerland)**
- Status: Warm but unverified
- Next: Follow-up outreach

**Bill McBane**
- Status: Potential introduction source for FBO network
- Next: Ask for 3-5 FBO operator intros

### FBO Distribution Channel
- Massive FBO presence at NBAA SDC Cleveland confirmed
- 20 operator outreach list with pitch angles drafted
- Strategy: Collect operator names, warm intros via FBOs

### Trade Shows
- ✅ NBAA SDC Cleveland (Mar 24-26) — attended, pitch NOT market-ready
- 🎯 NBAA-BACE October 2026 — target (25K attendees, critical for scaling)
- 🔮 SDC Fort Lauderdale Feb 2027 — backup

### Messaging (Locked)
- **Core:** "Tell us what you need. We handle the rest."
- **Subline:** "We're making charter aviation much easier. One conversation at a time."
- **What You DON'T Sell:** AI, cheap flights, or technology
- **What You DO Sell:** Fair pricing, transparency, ease, operator liberation
- **Voice:** Direct, punchy, human, confident (not arrogant), playful. No jargon ("leverage," "optimize").
- **Feel:** Warm, honest, easy, approachable, reliable, disruptive

### Positioning Strategies Explored
1. **Redline Agency:** "Prosecution → Evidence → Verdict → Action" (justice against industry)
2. **Groundswell Creative:** "Operator Pain → Operator Liberation → Passenger Benefit"
3. **Passenger Zero:** "Curiosity → Demystification → Permission → Action" (private aviation for first-timers)
4. **Disruption Collective:** Radical transparency, anti-broker movement
5. **Quietude:** "Private aviation without the performance" (desire-based, exclusive positioning)

**Assessment:** Strategies drafted but not tested. Founder pitch at NBAA Cleveland wasn't market-ready.

---

## TARGET CUSTOMERS

**Primary Segments:**
1. HNW individuals (high-net-worth charter buyers)
2. Corporate travel managers
3. Family groups
4. Part 135 operators (1-20 aircraft)

**Customer Acquisition:**
- Direct: Bryce Cannon (test case)
- Channel: FBOs (20+ operator outreach list)
- Trade shows: NBAA-BACE (Oct 2026)

**Success Criterion:** One person successfully books a flight end-to-end through Wingman (with a real or test operator) by May 31, 2026.

---

## CRITICAL DECISIONS NEEDED

### By April 15
1. **Bryce Cannon Status** — Converting or stalling? If stalling, move to Lazo immediately.
2. **Pipeline Fix ETA** — When is it live? (This blocks everything: QA, Audit, task verification)
3. **Pricing Feature** — Build in-house or partner? (Tivoli pricing May 2026; you're 6 weeks behind)

### By April 30
1. **Empty Legs Feature** — Spec, design, queue for build
2. **Cargo Module** — Initial spec (identified as top revenue source)
3. **SPEC.md Rewrite** — Cancellation tiers, AI moderation, operator vetting logic
4. **Adam Transition Plan** — Who owns operator acquisition now? (You? Hire? Defer 90 days?)

### By June 30
1. **NBAA-BACE Strategy** — Booth? Speaking slot? Demo-ready product?
2. **First Operator Onboarded** — Bryce or Lazo must be live and taking bookings
3. **Pricing Engine Live** — Competitive with or ahead of Tivoli (May launch)
4. **End-to-End User Test** — 1 person books a flight via Wingman successfully

### By Q1 2027
1. **$300K Revenue or Pivot Decision** — Extend runway or shift to SaaS model (30-40% higher success probability)

---

## PRIORITY BACKLOG (For Dev)

### P0 (Blocking)
1. **Fix Pipeline** — Gremlin QA, Audit, task verification (by Apr 30)
2. **Pricing Engine** — Spec, build, test (by May 31, before Tivoli)
3. **End-to-End User Flow Test** — 1 real booking (by May 31)

### P1 (Critical)
1. **Wingman Session History** (W-003 subfeature)
2. **W-003b: Anonymous Wingman** (allow anonymous conversations)
3. **W-003c: Confirmation Flow** (verify booking details before submission)
4. **Empty Legs Module** — Spec + MVP (speed advantage)
5. **Cargo Module** — Initial spec (revenue potential)
6. **SPEC.md Rewrite** — Cancellation tiers, AI moderation, vetting logic

### P2 (Nice-to-Have)
1. W-006, W-007, W-008 (Omnichannel, channel switching, Wingman-first landing)
2. Live deals carousel
3. Conversation carousels in Wingman panel
4. Mobile app (if demand signals warrant)

### Known Bugs to Fix
1. Chat scrolling (affects UX)
2. Notification dropping (silent failures)
3. User management errors (operator admin workflows broken)
4. Operator approvals API (intermittent failures)

---

## RUNWAY & FINANCIAL CONSTRAINTS

**Monthly Burn:** $500-700  
**Runway:** ~12 months (assumes no hiring, no infrastructure scaling)  
**Anthropic API:** Pay-as-you-go (crons on Gemma4; zero cost)  
**AWS:** ~$350/mo (compute, storage, data transfer)

**Revenue Timeline:**
- **0 months (now):** $0
- **6 months (Oct 2026):** Must have 1+ operators live, booking volume trending
- **12 months (Apr 2027):** $300-400K revenue or runway expires

---

## KNOWN UNKNOWNS

1. **Hetzner Cost** — Needed for exact burn rate calculation
2. **Operator Vetting Logic** — Trust score formula; how many operators can you onboard in parallel?
3. **Cancellation Tiers** — What happens if operator cancels? Refund policy unclear.
4. **AI Moderation** — Who flags unsafe flights? What are the rules?
5. **Pricing Rules** — How do operators set base rates? Dynamic pricing? Margins?
6. **Empty Legs Matching** — How do you match empty legs to passengers? Algorithm undefined.
7. **Cargo Integration** — How do cargo requests flow into Wingman? Separate workflow?
8. **Payment Flow** — Wire/ACH integration for operator payouts? Current implementation?

---

## RECENT INTEL FROM NBAA SDC CLEVELAND (Mar 24-26)

- **Hamilton AI in person:** Auto-quote live, $10M raised, email-first workflow
- **Tivoli rep:** Pricing engine launching May 2026, ~4K operators global
- **FBO landscape:** Massive presence; potential distribution channel for operator sourcing
- **Competitive takeaway:** Email-centric workflows are Hamilton & Tivoli's weakness. Your Wingman advantage if executed well.

---

## KEY CONTACTS

**Business:**
- Jack Bradham: jack@goflight.ai (M365), jackb@live.com (Outlook)
- Bryce Cannon (Vantage Air): Bcanon@vantageair.com
- Lazo Qaradaxi (NBAA Cleveland lead): [Contact TBD]
- Bill McBane (FBO intro source): [Contact TBD]
- Jacob (Switzerland operator): [Contact TBD]

**Competitors:**
- Hamilton AI: Wouter Witvoet (wouter@hamilton.ai, 302-563-3823)
- Tivoli: [Pricing launch May 2026]

**CPA (Taxes/Financials):**
- Kermit Bolick (Huggins CPA): kkbolick@hugginscpa.com

---

## REFERENCE DOCS

- **SPEC.md:** GoFlight/SPEC.md (needs rewrite for clarity)
- **CLAUDE.md:** GoFlight/CLAUDE.md (project-wide AI context)
- **Task Board:** https://nerds.struktproto.com (Task Board + Factory Output tabs)
- **Operating Plan:** https://nerds.struktproto.com/share/operating-plan.html
- **Business Review:** https://nerds.struktproto.com/share/business-review.html

---

## THE HONEST TRUTH

GoFlight is infrastructure-advanced but commercially unproven. You have 6 weeks before Tivoli prices (your speed advantage evaporates). You need one operator converting and one end-to-end booking by May 31. The pipeline being down is costing you velocity. Adam's departure means you're solo on GTM — that's either a feature (clarity, speed) or a bug (no division of labor).

**Window:** Oct 2026 NBAA-BACE is your distribution play. Everything between now and then is prep.

---

**Document updated:** April 10, 2026 22:30 ET  
**For:** Claude Code sessions, Runway/Pixel/Lander briefings, investor/partner discussions
