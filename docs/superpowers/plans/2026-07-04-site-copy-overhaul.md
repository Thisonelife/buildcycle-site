# Site Copy Overhaul Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rewrite buildcycle.io copy to sell to the architect, arm them for the principal, reassure the operator — waitlist-coherent with `AT-LAUNCH` flip comments — and split Procore developer-program material onto an unlinked partner page.

**Architecture:** Plain static HTML — every change is an exact text replacement in one of five HTML files plus one new page built from `_shell.html`. No CSS, JS, asset, or nav changes (one exception: two new same-page anchor links). Every displaced trial string is preserved in an adjacent `<!-- AT-LAUNCH: ... -->` comment.

**Tech Stack:** Hand-edited HTML, existing `styles.css` classes only. Repo `/Users/thisonelife/dev/buildcycle/site`, deploys to buildcycle.io on push (Cloudflare Pages) — **do NOT push; Brad reviews first.**

**Spec:** `docs/superpowers/specs/2026-07-04-site-copy-overhaul-design.md`

## Global Constraints

- Copy only. No layout/CSS/JS/asset/nav changes beyond what a task explicitly shows.
- Waitlist-coherent everywhere; every displaced trial string parked verbatim as `<!-- AT-LAUNCH: <original html> -->` immediately after its replacement.
- Professional tier flag is exactly `Most firms start here` everywhere.
- Contact email is exactly `support@buildcycle.io` everywhere (replaces `info@buildcycle.io`).
- The new partner page is `procore-partner.html`, carries `<meta name="robots" content="noindex">`, and is linked from NOWHERE.
- HTML entities follow the site's existing style (`&mdash;`, `&rsquo;`, `&middot;`).
- Do NOT push to origin at any point — Brad reviews the rendered site locally first (`open index.html` or a local server).

---

### Task 1: index.html — hero, ticker, cards, pricing teaser, waitlist section

**Files:**
- Modify: `index.html`

**Interfaces:**
- Produces: anchor expectation — the pricing-section paragraph links to `/pricing.html#seat-math` (Task 2 creates that id).

- [ ] **Step 1: Hero micro-line (waitlist-true, park trial)**

Replace (line ~65):
```html
        <span class="micro">No credit card required</span>
```
with:
```html
        <span class="micro">Early access &mdash; onboarding firms now</span>
        <!-- AT-LAUNCH: <span class="micro">No credit card required</span> -->
```

- [ ] **Step 2: Ticker — drop "A third of the price" (both loop copies)**

In BOTH ticker lines (~98 and ~99), replace:
```html
<span>A third of the price</span>
```
with:
```html
<span>Priced by projects, not people</span>
```

- [ ] **Step 3: Card 02 — outcome-first close**

Replace:
```html
        <p>Change orders with a two-signature lifecycle and live contract math. Pay applications reviewed and certified without the spreadsheet ritual.</p>
```
with:
```html
        <p>Change orders with a two-signature lifecycle. Pay applications reviewed and certified without the spreadsheet ritual. The contract value is always current &mdash; nobody does month-end archaeology.</p>
```

- [ ] **Step 4: Card 03 — the record leaves with you (export tie-in)**

Replace:
```html
        <p>Field reports that build themselves into clean PDFs — weather attached — and punch lists that actually close out.</p>
        <ul class="spec">
          <li>Field reports — PDF + weather</li>
          <li>Punch lists — open to verified</li>
          <li>Site record — defensible, dated</li>
        </ul>
```
with:
```html
        <p>Field reports that build themselves into clean PDFs &mdash; weather attached &mdash; and punch lists that actually close out. When the job ends, the whole record exports as one zip. It leaves with you.</p>
        <ul class="spec">
          <li>Field reports — PDF + weather</li>
          <li>Punch lists — open to verified</li>
          <li>Export — the full record, one zip</li>
        </ul>
```
(Card 01 is untouched — "a paper trail your insurer would frame" already carries the risk argument.)

- [ ] **Step 5: Pricing-section paragraph — principal hook + seat-math link**

Replace:
```html
      <p>Priced by active projects — never by seats. Your consultants, the GC, the owner&rsquo;s rep: all of them collaborate at no charge, on every plan.</p>
```
with:
```html
      <p>Priced by active projects — never by seats. Your consultants, the GC, the owner&rsquo;s rep: all of them collaborate at no charge, on every plan. Need to convince the person who signs? <a href="/pricing.html#seat-math" style="color:var(--yellow);">Do the seat math</a>.</p>
```

- [ ] **Step 6: Pricing teaser foot (waitlist-true, park trial)**

Replace:
```html
    <p class="pricing-foot rv">30-day free trial of Professional &nbsp;&middot;&nbsp; <b>No credit card required</b> &nbsp;&middot;&nbsp; <a href="/pricing.html" style="color:var(--yellow);">Full pricing details</a></p>
```
with:
```html
    <p class="pricing-foot rv">Every plan: <b>all features, unlimited users</b> &nbsp;&middot;&nbsp; <a href="/pricing.html" style="color:var(--yellow);">Full pricing details</a></p>
    <!-- AT-LAUNCH: <p class="pricing-foot rv">30-day free trial of Professional &nbsp;&middot;&nbsp; <b>No credit card required</b> &nbsp;&middot;&nbsp; <a href="/pricing.html" style="color:var(--yellow);">Full pricing details</a></p> -->
```

- [ ] **Step 7: Waitlist section — early-access framing**

Replace:
```html
      <h2>Not ready yet?</h2>
      <p>Get BuildCycle updates — no spam, launch news only. One email when something ships that matters.</p>
```
with:
```html
      <h2>Get in line.</h2>
      <p>BuildCycle is onboarding early firms now. Join the list and you&rsquo;ll get one email when your spot opens &mdash; no spam, launch news only.</p>
```

- [ ] **Step 8: Verify + commit**

Run: `grep -n "free trial\|No credit card" index.html` — every hit must be inside an `AT-LAUNCH` comment. Run: `grep -c "A third of the price" index.html` → 0. Open the page (`open index.html`) and eyeball the hero, ticker, cards, pricing, waitlist sections.

```bash
git add index.html
git commit -m "copy(index): waitlist-coherent hero/pricing, outcome-first cards, seat-math hook, early-access framing"
```

---

### Task 2: pricing.html — seat-math ROI section, tier flag, Q&A, waitlist coherence

**Files:**
- Modify: `pricing.html`

**Interfaces:**
- Produces: `id="seat-math"` section (consumed by index.html link from Task 1).

- [ ] **Step 1: Unify Professional flag**

Replace:
```html
        <span class="tier-flag">Most specified</span>
```
with:
```html
        <span class="tier-flag">Most firms start here</span>
```

- [ ] **Step 2: Tiers foot (waitlist-true, park trial)**

Replace:
```html
    <p class="pricing-foot rv in">30-day Professional trial &nbsp;&middot;&nbsp; <b>No credit card</b></p>
```
with:
```html
    <p class="pricing-foot rv in">Every plan: <b>all features, unlimited users, Procore sync included</b></p>
    <!-- AT-LAUNCH: <p class="pricing-foot rv in">30-day Professional trial &nbsp;&middot;&nbsp; <b>No credit card</b></p> -->
```

- [ ] **Step 3: Insert the "Do the seat math" section**

Immediately AFTER the comparison band's closing (`</section>` following the `$0 / seat` band, line ~185) and BEFORE `<!-- ================= STRAIGHT ANSWERS ================= -->`, insert:

```html
<!-- ================= SEAT MATH (ROI) ================= -->
<section class="sec-dark sec-pad" id="seat-math">
  <div class="wrap">
    <div class="sec-head sec-head--dark rv">
      <div>
        <span class="tag"><b>SEC. 02</b> &nbsp;/&nbsp; Do the seat math</span>
        <h2>Show this to<br><span class="pale">the person who signs.</span></h2>
      </div>
      <p>Construction administration is the phase that quietly eats the fee — and the software for it is usually priced per seat, so every consultant added to the job raises the bill and teams leave people out. BuildCycle is priced by active projects: the whole team, in-house and out, works under one flat price, and answers move instead of waiting on someone&rsquo;s license.</p>
    </div>

    <div class="tiers" style="grid-template-columns: repeat(2, minmax(0,1fr)); max-width: 860px;">
      <div class="tier rv">
        <div class="tier-name">Per-seat tools</div>
        <div class="tier-scope">12-person project team</div>
        <div class="tier-price">$300&ndash;$1,500<small>/ mo</small></div>
        <ul class="tier-feats">
          <li>$25&ndash;$125 per user, per month</li>
          <li>Consultants need paid seats — or stay outside the system</li>
          <li>$3,600&ndash;$18,000 a year, per team</li>
        </ul>
      </div>

      <div class="tier tier--hot rv rv-d1">
        <span class="tier-flag">Same team, flat</span>
        <div class="tier-name">BuildCycle</div>
        <div class="tier-scope">Same 12-person team</div>
        <div class="tier-price">$199<small>/ mo</small></div>
        <ul class="tier-feats">
          <li>Professional — 10 active projects, flat</li>
          <li>Consultants, GC, owner&rsquo;s rep: $0, inside the system</li>
          <li>$1,990 a year on annual billing</li>
        </ul>
      </div>
    </div>

    <p class="pricing-foot rv">And the record is the firm&rsquo;s: every answer timestamped, every approval logged, the whole project exportable as one zip when the job closes.</p>
  </div>
</section>
```

- [ ] **Step 4: Renumber "Straight answers" section tag**

Replace:
```html
        <span class="tag"><b>SEC. 02</b> &nbsp;/&nbsp; Straight answers</span>
```
with:
```html
        <span class="tag"><b>SEC. 03</b> &nbsp;/&nbsp; Straight answers</span>
```

- [ ] **Step 5: Q.02 — swap trial question for the operator question (park trial Q&A)**

Replace:
```html
      <div class="qa rv">
        <span class="qa-num" aria-hidden="true">Q.02</span>
        <div>
          <h3>What happens when my trial ends?</h3>
          <p>Day 31 the workspace becomes read-only: everything visible and exportable, nothing editable until you pick a plan. <b>Your data is never deleted.</b></p>
        </div>
      </div>
```
with:
```html
      <div class="qa rv">
        <span class="qa-num" aria-hidden="true">Q.02</span>
        <div>
          <h3>What does rollout actually look like?</h3>
          <p>Minutes, not months. No server, no IT project, no implementation consultant. Your team signs in, your consultants accept a free invite, and Procore connects per-project with OAuth. <b>The office manager never audits a seat count again.</b></p>
        </div>
      </div>
      <!-- AT-LAUNCH: restore trial Q&A —
      <div class="qa rv">
        <span class="qa-num" aria-hidden="true">Q.02</span>
        <div>
          <h3>What happens when my trial ends?</h3>
          <p>Day 31 the workspace becomes read-only: everything visible and exportable, nothing editable until you pick a plan. <b>Your data is never deleted.</b></p>
        </div>
      </div>
      -->
```
(Note: at launch both questions can coexist as Q.02/Q.06 — flip decision then. Q.01/Q.03/Q.04/Q.05 are unchanged.)

- [ ] **Step 6: Closing CTA micro (waitlist-true, park trial)**

Replace:
```html
      <span class="micro">30-day Professional trial &middot; No credit card</span>
```
with:
```html
      <span class="micro">Flat price &middot; Whole team included</span>
      <!-- AT-LAUNCH: <span class="micro">30-day Professional trial &middot; No credit card</span> -->
```

- [ ] **Step 7: Verify + commit**

Run: `grep -n "trial\|No credit card" pricing.html` — hits only inside `AT-LAUNCH` comments. `grep -c "Most specified" pricing.html` → 0. `grep -n 'id="seat-math"' pricing.html` → 1 hit. Open the page and check the seat-math section renders with two cards side by side and the billing toggle still works (it targets `.amt/.per` within `#plans`, untouched).

```bash
git add pricing.html
git commit -m "copy(pricing): seat-math ROI section, unified tier flag, operator Q&A, waitlist-coherent"
```

---

### Task 3: procore-integration.html — trust reframe, remove program section, CTA

**Files:**
- Modify: `procore-integration.html`

**Interfaces:**
- Consumes: nothing. Produces: the removed "Support commitments" content reappears on `procore-partner.html` (Task 4 contains it verbatim — Task 4 does not read this file).

- [ ] **Step 1: Hero micro (waitlist/value-true, park trial)**

Replace:
```html
      <span class="micro">No credit card required</span>
```
with:
```html
      <span class="micro">Included on every plan &mdash; nothing extra to buy</span>
      <!-- AT-LAUNCH: <span class="micro">No credit card required</span> -->
```

- [ ] **Step 2: Engineering principles → buyer trust framing**

Replace:
```html
        <span class="tag"><b>SEC. 03</b> &nbsp;/&nbsp; Engineering principles</span>
        <h2>Built to be<br><span class="pale">trusted.</span></h2>
```
with:
```html
        <span class="tag"><b>SEC. 03</b> &nbsp;/&nbsp; Ground rules</span>
        <h2>Your GC&rsquo;s record.<br><span class="pale">Still theirs.</span></h2>
```
and replace the section's lead paragraph:
```html
      <p>Four rules the integration never breaks &mdash; written for the GC who owns the Procore record as much as for the design team responding to it.</p>
```
with:
```html
      <p>The first question every GC asks: &ldquo;is this going to touch our Procore?&rdquo; Only the ways they&rsquo;d want. Four rules the integration never breaks &mdash; forward this section to your GC.</p>
```
(The four `prin` blocks — Status stays yours / No deletes / Formal actions only / No duplicate entry — are already buyer-grade. Leave all four untouched.)

- [ ] **Step 3: Remove the Support commitments section**

Delete the ENTIRE block from:
```html
<!-- ================= SUPPORT COMMITMENTS ================= -->
```
through its closing `</section>` (the block containing "Maintained. In writing.", the four `commits` list items, and support@buildcycle.io). Leave no gap comment — Task 4's page now owns this content.

- [ ] **Step 4: CTA band (waitlist-true, park trial headline)**

Replace:
```html
      <h2>Start your 30-day free trial</h2>
      <p class="cta-note">No credit card required &middot; Unlimited users on every plan</p>
```
with:
```html
      <h2>Bring CA back to the design side</h2>
      <p class="cta-note">Included on every plan &middot; Unlimited users &middot; Early access now</p>
      <!-- AT-LAUNCH: <h2>Start your 30-day free trial</h2><p class="cta-note">No credit card required &middot; Unlimited users on every plan</p> -->
```

- [ ] **Step 5: Verify + commit**

Run: `grep -n "trial\|No credit card" procore-integration.html` — hits only in `AT-LAUNCH` comments. `grep -c "Support commitments\|Maintained\." procore-integration.html` → 0. `grep -c "prin-stamp" procore-integration.html` → 4 (all four principles intact). Open the page: SEC.03 reads as trust copy; page ends workflow → how-it-works → ground rules → CTA.

```bash
git add procore-integration.html
git commit -m "copy(procore): principles reframed as buyer trust copy; program SLA section moved off-page; waitlist-true CTA"
```

---

### Task 4: Create procore-partner.html (unlinked, noindex)

**Files:**
- Create: `procore-partner.html` (start from `_shell.html` per its own header instructions: copy, replace title/meta, replace between PAGE CONTENT markers)

**Interfaces:**
- Consumes: `_shell.html` scaffold (shared nav/footer/JS included).
- Produces: nothing consumed elsewhere. NO page may link here.

- [ ] **Step 1: Copy the shell**

```bash
cp _shell.html procore-partner.html
```

- [ ] **Step 2: Head block**

Set `<title>Procore Partner Information — BuildCycle</title>`; set meta description and og tags to `Support commitments and integration principles for the BuildCycle Procore integration — partner and marketplace reference.`; ADD directly under the viewport meta:
```html
<meta name="robots" content="noindex">
```

- [ ] **Step 3: Page content (between `<!-- PAGE CONTENT -->` markers)**

```html
<!-- ================= PARTNER HERO ================= -->
<section class="sec-dark sec-pad" style="padding-top: calc(var(--nav-h) + 80px);">
  <div class="wrap">
    <div class="sec-head sec-head--dark rv in">
      <div>
        <span class="tag"><b>PARTNER</b> &nbsp;/&nbsp; Procore integration reference</span>
        <h2>Maintained.<br><span class="pale">In writing.</span></h2>
      </div>
      <p>Support commitments and engineering principles for the BuildCycle + Procore integration. These are public commitments, not aspirations &mdash; hold us to them.</p>
    </div>

    <ul class="commits rv" style="margin-top: 24px;">
      <li>
        <span class="commit-k">Support tickets</span>
        <span class="commit-v">Same-day response on integration support tickets during business hours.</span>
      </li>
      <li>
        <span class="commit-k">Breaking changes</span>
        <span class="commit-v">Response within 7 days to any Procore breaking-change notice.</span>
      </li>
      <li>
        <span class="commit-k">Who maintains it</span>
        <span class="commit-v">The integration is maintained directly by the founder &mdash; a practicing architect.</span>
      </li>
      <li>
        <span class="commit-k">Contact</span>
        <span class="commit-v"><a href="mailto:support@buildcycle.io">support@buildcycle.io</a></span>
      </li>
    </ul>
  </div>
</section>

<!-- ================= PRINCIPLES + CONNECTION MODEL ================= -->
<section class="sec-concrete sec-pad">
  <div class="wrap">
    <div class="sec-head rv">
      <div>
        <span class="tag"><b>REF. 01</b> &nbsp;/&nbsp; Integration principles</span>
        <h2>Four rules.<br><span class="pale">Never broken.</span></h2>
      </div>
      <p>BuildCycle never modifies Procore item status (status belongs to the record owner). The integration performs zero delete operations in Procore. Responses post exclusively as formal actions &mdash; official RFI replies and submittal approver responses, never comments. Data is written once in BuildCycle and delivered to Procore programmatically.</p>
    </div>
    <div class="sec-head rv" style="margin-top: 8px;">
      <div>
        <span class="tag"><b>REF. 02</b> &nbsp;/&nbsp; Connection model</span>
        <h2>OAuth 2.0.<br><span class="pale">Per project.</span></h2>
      </div>
      <p>Each Procore project is linked individually via OAuth 2.0 from BuildCycle&rsquo;s integrations page, using the connected Procore account&rsquo;s own permissions. Open RFIs and submittals &mdash; with approver workflows and attachments &mdash; sync in on connect and refresh during use. Full product details: <a href="/procore-integration.html">buildcycle.io/procore-integration</a>.</p>
    </div>
  </div>
</section>
```

Note: the `commits` list styles live in `procore-integration.html`'s inline `<style>` block, not `styles.css`. Copy that small CSS block (`.commits`, `.commit-k`, `.commit-v` rules) into this page's `<style>` section inside `<head>` (the shell has a spot for page-specific styles; if not, add a `<style>` block after the stylesheet link).

- [ ] **Step 4: Verify + commit**

Open `procore-partner.html`: nav/footer render, commitments list styled, noindex present (`grep -c 'name="robots"' procore-partner.html` → 1). Confirm NOTHING links to it: `grep -rn "procore-partner" index.html pricing.html procore-integration.html terms.html privacy.html _shell.html` → zero hits.

```bash
git add procore-partner.html
git commit -m "feat(site): unlinked noindex procore-partner page — program support commitments + integration reference"
```

---

### Task 5: Legal light touch — terms.html + privacy.html

**Files:**
- Modify: `terms.html:188,209,296`
- Modify: `privacy.html:174,263,277`

- [ ] **Step 1: terms.html — product description (×2)**

Line ~188, replace `a project management application for architects and engineers` with `a construction administration platform for architects, engineers, and design teams`.

Line ~209, replace:
```html
        <dd>means the BuildCycle project management application, including its features for tracking document progress, recording project updates via photos, managing users and organizations, and storing files in a multi-tenant environment.</dd>
```
with:
```html
        <dd>means the BuildCycle construction administration platform, including its features for managing RFIs, submittals, change orders, pay applications, field reports, and punch lists; recording project updates via photos; managing users and organizations; and storing files in a multi-tenant environment.</dd>
```

- [ ] **Step 2: terms.html — contact email**

Line ~296: replace both occurrences of `info@buildcycle.io` in the contact line (mailto href + display text) with `support@buildcycle.io`.

- [ ] **Step 3: privacy.html — product description + emails**

Line ~174: replace `project management application for architects, engineers, and construction professionals` with `construction administration platform for architects, engineers, and construction professionals`.
Lines ~263 and ~277: replace `info@buildcycle.io` with `support@buildcycle.io` (href + display text, all occurrences).

- [ ] **Step 4: Verify + commit**

Run: `grep -rn "info@buildcycle.io" *.html` → zero hits. `grep -rn "project management application" *.html` → zero hits. The "sample Terms" disclaimer note must still be present (`grep -c "not legal advice" terms.html` → 1) — it stays until real counsel.

```bash
git add terms.html privacy.html
git commit -m "copy(legal): align product description with CA positioning; unify contact to support@"
```

---

### Task 6: Site-wide acceptance sweep

**Files:** none created; verification only.

- [ ] **Step 1: Acceptance greps (all must pass)**

```bash
# trial promises only inside AT-LAUNCH comments:
grep -rn "free trial\|Free Trial\|No credit card" *.html | grep -v "AT-LAUNCH"   # → empty
# one tier label:
grep -rn "Most specified" *.html                                                 # → empty
grep -rc "Most firms start here" index.html pricing.html                         # → 1 and 1
# one contact email:
grep -rn "info@buildcycle.io" *.html                                              # → empty
# partner page unlinked + noindex:
grep -rn "procore-partner" index.html pricing.html procore-integration.html terms.html privacy.html _shell.html  # → empty
grep -c 'name="robots" content="noindex"' procore-partner.html                    # → 1
# seat-math anchor pair:
grep -c 'pricing.html#seat-math' index.html                                       # → 1
grep -c 'id="seat-math"' pricing.html                                             # → 1
```

- [ ] **Step 2: Visual pass**

`open index.html pricing.html procore-integration.html procore-partner.html` — check: seat-math cards render two-up; procore page flows workflow → steps → ground rules → CTA with no orphan spacing where the support section was; partner page nav/footer intact.

- [ ] **Step 3: Final commit (if any stragglers) — do NOT push**

Brad reads all pages before push. Push = deploy.
