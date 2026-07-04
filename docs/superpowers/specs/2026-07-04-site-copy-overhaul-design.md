# BuildCycle.io Copy Overhaul — Design

**Date:** 2026-07-04
**Status:** Design approved by Brad (pending spec review)
**Repo:** `~/dev/buildcycle/site` (plain static HTML/CSS, no build step, Cloudflare Pages auto-deploy on push)
**Notion:** "Site wording revision pass (Brad's list)" + "Fix site trial wording after waitlist switch"

## Goal

Rewrite the site's copy to sell — to the end user (project architect), with
ammo they can carry to the decision maker (principal), and reassurance for
the firm operator — while keeping the existing Hi-Vis design, layout, and
nav untouched. Fix the waitlist/trial incoherence. Strip Procore
developer-program material from the sales narrative without losing it.

## Constraints (locked with Brad)

- **Design stays.** No layout, color, font, nav, or asset changes. Copy only
  (plus one new unlinked page and one new pricing-page block using existing
  CSS components).
- **CTA state: waitlist now, flip-ready.** All visible copy reads coherently
  for the waitlist-gated state. Launch-day trial wording is written NOW and
  parked adjacent in `<!-- AT-LAUNCH: ... -->` comments. Launch flip = grep
  `AT-LAUNCH`, swap, delete comments.
- **Procore split:** "Engineering principles" STAYS on
  `procore-integration.html`, rewritten as buyer-facing trust copy. "Support
  commitments" (SLAs, breaking-change response — developer-program material)
  MOVES to a new **unlinked** `/procore-partner.html` (reachable by URL for
  Procore reviewers; zero nav/footer presence).
- **Decision-maker ammo: woven + ROI block.** No new nav pages. Principal
  and operator arguments woven into index + pricing; one new "seat math"
  ROI block on pricing.html.
- **Branding: VERIFIED CURRENT 2026-07-04.** Every site brand asset
  (buildcycle-primary/inverse/mark SVGs, favicon 16–96 + .ico + .svg,
  apple-touch-icon, icon-192/512/maskable, site.webmanifest) hash-matches
  the latest `~/dev/buildcycle/BC logos` bundle byte-for-byte. No asset
  changes in this project.

## Messaging spine

Positioning line (kept): **the construction-administration platform for the
design side of the table.** The rewrite adds the argument ladder the site
currently lacks:

| Audience | Their question | Arguments the copy must land |
|---|---|---|
| Project architect (end user) | Will this make my CA week suck less? | One place for RFIs/submittals/COs/pay apps; money math done live; respond to Procore without living in Procore. (Current voice — keep it.) |
| Principal (decision maker) | Why spend $199/mo? | (1) **Fee protection** — CA quietly eats the fee; faster turnaround = fewer burned hours. (2) **Risk** — complete, timestamped, exportable record of every answer/approval = claims defense. (3) **Math** — flat vs per-seat: a 12-person team on $25–$125/seat tools runs $300–$1,500/mo before one consultant logs in; BuildCycle is $199 with everyone free. |
| Firm operator | What does this cost me in hassle? | No IT project (minutes to connect); no seat audits or license reconciliation; predictable flat bill; consultants onboard themselves free. |

Voice: keep the jobsite-confident register ("Built on job sites, not in
boardrooms"), short declarative headlines, AEC jargon unapologetic on
feature copy but every principal-facing argument in plain money/risk terms.

## Page-by-page

### index.html
- **Hero:** H1 unchanged ("Construction admin that answers to you.").
  Subhead tightened (keep flat pricing + everyone-collaborates-free).
  Micro-line under CTA: waitlist-true replacement for "No credit card
  required" (e.g. early-access framing); trial line parked in `AT-LAUNCH`.
- **Ticker:** drop "A third of the price" (unprovable as stated); replace
  with a defensible line; rest keeps rhythm.
- **Section 01 cards (Answer & track / Move the money / Hold the record):**
  outcome-first rewrites — each card ends with the so-what for the firm
  (time back, money visible, record defensible). "Hold the record" card
  gains the exportable-record point (ties to the new Export Archive
  feature: the record leaves with you, zip in hand).
- **Procore band:** copy kept, tightened; still links to integration page.
- **Pricing teaser:** unify Professional's flag (single label, see
  Consistency), waitlist-coherent foot line (`AT-LAUNCH` for trial line).
- **Waitlist section:** reframed from passive "Not ready yet?" to
  early-access truth — the waitlist is the only door right now. Keep
  "no spam, launch news only."

### pricing.html
- **Hero + tiers:** copy kept structurally; tier flag unified; foot lines
  waitlist-coherent with `AT-LAUNCH` parking.
- **NEW: "Do the seat math" ROI block** (existing comparison-band CSS):
  side-by-side — per-seat tool at 12 users ($25–$125/seat → $300–$1,500/mo,
  $3.6k–$18k/yr) vs BuildCycle Professional flat $199/mo ($1,990/yr),
  consultants/GC/owner's rep included at $0. One closing line addressed to
  the principal.
- **Q&A ("Straight answers"):** rewritten waitlist-coherent (trial-end Q&A
  parked in `AT-LAUNCH`); ADD one operator question ("What does rollout
  actually look like?" — connect in minutes, no IT project, team invites
  themselves); keep the consultant-license and Procore-included answers.
- **Closing CTA:** waitlist-true headline + micro.

### procore-integration.html
- **Hero / workflow / how-it-works:** copy tightened, sales-first; the
  four-step "No IT project" framing stays (it is operator ammo).
- **Engineering principles → buyer trust copy:** same four facts, reframed
  as answers to the GC's and principal's real objection ("will this mess up
  our Procore record?"): status never touched, nothing ever deleted, formal
  actions only, no duplicate entry. Section retitled accordingly.
- **Support commitments section REMOVED** from this page.
- **Closing CTA:** "Start your 30-day free trial." headline replaced with
  waitlist-true copy (`AT-LAUNCH` parks the trial version).

### NEW procore-partner.html (unlinked)
- Built from `_shell.html`. Contains the developer-program material:
  support commitments (same-day ticket response business hours; response
  within 7 days to Procore breaking-change notices; maintained by the
  founder, a practicing architect; support@buildcycle.io), plus a short
  restatement of the engineering principles and the OAuth/per-project
  connection model. Audience: Procore app-review/marketplace, not buyers.
  `<meta name="robots" content="noindex">`. No nav or footer links point
  to it anywhere on the site.

### terms.html / privacy.html (light touch ONLY)
- Product description aligned to the marketing positioning ("construction
  administration platform for design teams" instead of generic "project
  management application").
- Contact email unified (see Consistency).
- The visible "sample Terms … not legal advice" note STAYS — flagged for
  real counsel before launch, not fixed here. No other legal rewriting.

## Consistency sweep (all pages)
- **Professional tier flag:** one label everywhere — "Most firms start
  here" (home's version; warmer than "Most specified").
- **Contact email:** `support@buildcycle.io` everywhere, including legal
  pages (replaces `info@buildcycle.io`; Brad to ensure the alias exists).
- **Product name/description** identical across marketing + legal.
- All "start free trial" phrasing accounted for: replaced or `AT-LAUNCH`-parked.

## Flip-ready convention

Wherever waitlist copy displaced trial copy:

```html
<p class="cta-micro">Early access is rolling out firm by firm — join the list.</p>
<!-- AT-LAUNCH: <p class="cta-micro">30-day free trial of Professional · No credit card required</p> -->
```

One convention, greppable, deletable. The launch flip is a single pass.

## Out of scope
- Visual/layout/nav redesign; fonts, colors, assets (verified current).
- New indexed pages beyond the unlinked partner page.
- Real legal review of terms/privacy (flagged for counsel).
- Screenshots, demo video, or new imagery.
- App-side changes (kPublicSignupsEnabled etc.).

## Acceptance
- Every page reads coherently in the waitlist state; zero stranded trial
  promises outside `AT-LAUNCH` comments.
- `grep -ri "free trial" *.html` hits nothing outside `AT-LAUNCH` comments.
- Procore developer-program material absent from all nav-reachable pages;
  present and complete on /procore-partner.html.
- The pricing page contains the seat-math ROI block with defensible numbers.
- A principal reading only index + pricing encounters all three ammo
  arguments (fee, risk, math) without clicking anything.
- Brad reads every page and it sounds like BuildCycle, not like marketing.
