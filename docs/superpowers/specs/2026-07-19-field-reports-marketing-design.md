# Field Reports Marketing — /field-reports + /archisnapper-alternative

**Date:** 2026-07-19 · **Status:** Approved by Brad ("sounds right. build it")

## Why

Field reports were BuildCycle's origin (April MVP idea) and its most relatable wedge —
"architects spending hours writing reports in Word" — yet the site gives them two
bullet lines. Market: a real reports-only buyer segment exists (rForm sells site-report
projects at CAD $12.95; ArchiSnapper built a company on it). Brad names **ArchiSnapper
the #1 reporting competitor.**

## Deliverables

1. **/field-reports** — story/SEO page ("field report software for architects").
   Word-pain hero → plan-marker observations (SHIPPED: plan_markers table,
   observation_marker_picker) → what's in a report (auto NWS weather, photo archive,
   attendee record, PDF, CC distribution, export) → punch lists (open→verified ONLY —
   no plan-marker claim; BUI-56 unshipped) → "reports are the door, not the building"
   upsell → waitlist CTA.
2. **/archisnapper-alternative** — comparison page, same skeleton as part3/rform pages.
   Facts (July 2026 research): $34/user/mo ($29 annual), unlimited projects,
   reports+punch only, no RFIs/submittals/COs/pay apps; **now Deltek; public pricing
   REMOVED from vendor site — rates third-party-sourced (Capterra/GetApp), say so.**
   5-user firm ≈ $170/mo reports-only vs BC $79 (Starter) for everything.
   Honest wins: native mobile apps, offline, years of single-workflow polish.
3. **Homepage** card 03: link field-report line to /field-reports; keep copy tight.
   **pricing.html**: add ArchiSnapper to "Comparing options?" line.
   **sitemap**: + /field-reports (0.8), /archisnapper-alternative (0.7).

## Rules

Only shipped features in copy. Preview branch `field-reports-pages` → Brad review →
merge = deploy → request indexing in GSC.
