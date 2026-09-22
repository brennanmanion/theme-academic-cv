# SEO implementation and verification handoff

Prepared September 22, 2026 for https://cassidyartz.com/.
This is a plan only; this task does not authorize publication or change the site.

## Objective and success criteria

Increase qualified organic tutoring inquiries. Track five separate states for every changed URL: implemented, live, Google-accessible, indexed, and earning relevant search impressions/clicks. Track booking-page visits and confirmed bookings separately. A successful build, sitemap submission, or live inspection is not evidence of indexing or ranking.

Implementation can finish while Google processing is pending. Never label pending observations as passed, promise a ranking, or hold unrelated improvements indefinitely waiting for Google. Search changes may take days to weeks to be recrawled; indexing and serving are not guaranteed. [Google recrawl guidance](https://developers.google.com/search/docs/crawling-indexing/ask-google-to-recrawl).

## Inputs, skills, and limitations

- Repository: `/Users/brennan/Documents/theme-academic-cv`.
- Existing research: `docs/seo/sat-act-keyword-content-plan.md`. Treat its workbook-derived search volumes as historical estimates, not current verified demand or forecasts.
- Use `/Users/brennan/.codex/skills/hugo-theme/SKILL.md`, especially `references/seo-outputs-testing.md`, `references/template-architecture.md`, and `references/modules-and-performance.md`. There is no separate installed skill named “Hugo SEO”; SEO is a reference within the Hugo theme skill.
- Refinement from those references: inspect inherited Hugo Blox templates before overriding them; check generated HTML rather than trusting front matter; use narrowly scoped overrides and correct cache variants; verify production base URL, template selection, sitemap behavior, and deployed output.
- Netlify configuration pins Hugo 0.136.5 and invokes Hugo plus Pagefind. Skill examples include newer APIs: do not copy them without compatibility checks or bundle a Hugo/theme upgrade into SEO work.
- The homepage previously showed a duplicated service phrase in its title, unlinked service descriptions, and no visible service navigation. Recheck the live version before editing.
- Prior generated breadcrumbs appeared to contain extra quoted strings in names/URLs. Reproduce before fixing. LocalBusiness output was minimal; do not invent an address or assume the configured subtype is rendered.
- Earlier funnel code exists locally but deployment and completed-booking capture were not verified. Prior browser evaluation alone was insufficient to conclude GA4 is broken: confirm with actual browser network/debugger evidence.
- Some filesystem reads and Git commands stalled during this planning task. Inspect current state afresh; do not interpret absent tool output as a clean worktree or a successful build.
- No authenticated Search Console baseline was collected here. GA4/Windsor installation does not prove Search Console property access.

## Working rules

One numbered increment is one reviewable change/commit, normally one page or one technical behavior. After each change: inspect the diff, run relevant local checks, record the result, and then proceed. Deploy related low-risk increments in a small release when authorized; record precisely which commits share a release. If individual effect attribution matters, isolate releases and allow an observation window; tiny commits alone do not isolate SEO causality.

Preserve existing edits. Do not edit generated `public/` output as the source of a fix. Build in an isolated output/cache location or checkout; tracked generated files were changed/deleted by an earlier `--gc` build. Avoid cleanup commands over user files. Match the pinned Hugo version and production environment, and validate the complete Netlify pipeline including Pagefind before publication.

For each deployed increment use the verification gates below. Fixing a local defect does not authorize claiming it is live. Do not create another chat or an automation as part of this handoff.

## Small implementation increments

### Foundation: establish trustworthy evidence

1. **Record repository and deployment baseline.** Read applicable AGENTS.md, branch, working changes, remote, build configuration, deployed commit and Netlify production domain. Identify the templates that own title, description, canonical, robots directives and analytics. Output: a short baseline record with URLs and commit IDs; no site edits.
2. **Establish Search Console access and baseline.** Use the existing verified Domain property for cassidyartz.com if available, otherwise the matching HTTPS URL-prefix property. Record access role; request only missing access if necessary. Capture last complete 28 days versus preceding 28 days and 3 months of query/page data, with country/device filters recorded. Capture indexed status for homepage, test prep, admissions, testimonials and proposed new URLs. Missing data is “unavailable,” not zero. Output: dated baseline evidence.
3. **Inventory URLs and expected indexing.** Inspect live sitemap, robots.txt, response headers, canonical tags, legacy service URLs, `/schedule/`, `/lead-generation/`, `/confirmation/`, authors and taxonomies. Assign each URL: index, redirect, retain/noindex, or investigate. Recheck real legacy paths instead of inferring them from mixed-case content directories. Output: URL disposition table; no redirects yet.

### Measurement: repair only reproduced gaps

4. **Verify booking-page event.** Review the funnel hook and theme GA4 loader; test both booking routes in an appropriate preview. Confirm one `booking_page_view` per page load, CTA click capture, and GA4 receipt. Preserve normal link navigation. Scope debug mode to explicit testing. Do not add a duplicate GA loader. Gate: actual browser event/request evidence and GA4 DebugView receipt on the intended property when available.
5. **Remove false completion counting.** A direct visit to `/confirmation/` is not proof of a booking. Remove that automatic `generate_lead` fallback unless backed by a trustworthy booking signal. Remove invented monetary value/currency for a free introductory call. Gate: direct visits and refreshes never create a lead.
6. **Verify Calendly embed event delivery.** Current templates use a plain iframe; do not assume it emits the documented events. Observe a genuine non-submitting event such as event-type view or date/time selection with browser diagnostics. If absent, use Calendly's supported inline embed configuration, preserving layout and a usable fallback link. Update both applicable embed templates or share a partial only where justified. Gate: event observed from the actual iframe; no synthetic event mistaken for real proof.
7. **Harden completed-booking capture.** Accept only the expected Calendly origin AND the actual embed's `contentWindow`; allowlist the completed-event name. Keep invitee data and raw payloads out of GA4. Make deduplication tolerant of blocked storage, suppress repeated messages for the same booking, and allow a distinct later booking. Avoid copying query strings containing personal information into event parameters. Gate: isolated tests cover wrong origin/source, duplicates, blocked storage and direct confirmation visits. A real end-to-end completion still requires an authorized test appointment.
8. **Add CTA location labels.** Give each homepage CTA a stable location (hero, services, results, footer, etc.) and identify service-page/navigation links. Gate: two buttons with identical wording produce distinguishable locations without changing navigation.
9. **Configure reports after event verification.** Mark genuine `generate_lead` as a GA4 key event; register only useful custom dimensions such as CTA location. Use booking-page visits as the initial interest metric, never as confirmed bookings. Record test traffic exclusions and property settings. Gate: a reproducible funnel report and definitions, with limitations documented. Measurement does not block independent SEO edits.

### Existing pages: low-risk visibility and relevance

10. **Fix homepage title duplication only.** Intended title: `Online SAT & ACT Tutoring | Cassidy Artz`. Inspect the actual Hugo Blox title construction and `{brand}` substitution. Gate: one rendered title, no duplicate brand/service suffix; sample inner-page titles unchanged unless explicitly intended.
11. **Refine homepage description only.** Write one accurate, distinct description conveying private online SAT/ACT tutoring and the complimentary introductory call. Gate: one description plus consistent social metadata; no keyword list or unverified promises.
12. **Clarify homepage opening copy only.** Bring online and one-on-one tutoring into the H1 or first paragraph. Proposed H1: `One-on-One Online SAT & ACT Tutoring`. Maintain the actual offer; avoid implying guaranteed Ivy League admission. Gate: visible mobile/desktop copy and coherent heading hierarchy.
13. **Link homepage SAT/ACT service descriptions.** Initially point to the existing `/test-prep/` page, with descriptive anchors. Gate: real HTML anchors present in response source; destination returns 200.
14. **Link homepage admissions description.** Point to `/college-admissions/`. Same source and destination checks.
15. **Link homepage proof section to testimonials.** Add one descriptive link to `/testimonials/`; retain booking CTA. Same checks plus keyboard/mobile usability.
16. **Correct breadcrumb serialization if reproduced.** In `layouts/partials/jsonld/main.html`, build structured values and serialize once using APIs supported by Hugo 0.136.5. Gate: JSON parses, names contain no literal wrapping quotes, item URLs are valid absolute production URLs; test two page depths and Rich Results Test. No assumed ranking uplift.
17. **Correct entity schema if evidence requires it.** Inspect inherited business/website partials. Represent the real person/business using accurate supported fields; do not manufacture a physical business location. Gate: schema parses and matches visible facts; valid schema alone does not guarantee a rich result.
18. **Expand test-prep page with verified process details.** Add session format, diagnostic approach, expected homework, parent communication and how pricing is discussed. Confirm facts with Cassidy where absent. Gate: useful specific content, unique title/description, clear scheduling link; do not invent rates or outcomes.
19. **Expand admissions page separately.** Explain actual scope, process, suitable timelines and boundaries of essay coaching. Gate: unique useful content with a clear consultation CTA and only approved facts.
20. **Audit proof and image presentation.** Verify testimonials, score statistics, consent and credentials. Show representative-image labels where appropriate; replace/remove claims that cannot be substantiated. Gate: each material claim has an owner-approved source. Missing proof blocks that claim, not unrelated technical work.

### URL hygiene: conditional, one target at a time

21. **Consolidate one confirmed duplicate service URL.** Use the inventory and Search Console history to select the destination; preserve unique useful content first. Add a permanent host redirect, update links and remove the old URL from sitemap. Repeat as a separate increment for each additional duplicate. Gate: one redirect hop to the intended 200/self-canonical page; no loop or homepage catch-all. Google should eventually index the destination, not both copies.
22. **Consolidate booking routes if equivalent.** Prefer `/schedule/` for internal links; verify embed behavior before redirecting `/lead-generation/`. Gate: old links still reach booking and the page event remains correct. Do not require booking pages to rank for tutoring queries.
23. **Exclude confirmation from indexing.** Render noindex and omit it from sitemap; keep it crawlable so Google can see noindex. Review thin utility/taxonomy pages individually in subsequent increments. Gate: directive present in live HTML/headers, absent from sitemap, eventually excluded in Search Console for the intended reason.
24. **Repair sitemap/canonical defects only if present.** Include intended canonical 200/indexable URLs; ensure absolute production domain URLs and truthful lastmod values. Test Hugo 0.136.5 exclusion behavior rather than assuming a front-matter flag works. Netlify's production `-b $URL` must resolve to the intended custom domain. Gate: parsed live XML and headers agree with URL inventory. Do not tune priority/changefreq as a ranking tactic or set lastmod to every build time.

### New content: each page is a separate release candidate

25. **Draft SAT Math page.** Proposed `/sat-math-tutor-online/`. Use the existing keyword brief, Cassidy's verified methods, who benefits, FAQs, and an approved example if available. Keep it draft until facts are ready. Gate: distinct intent from `/test-prep/`, no invented credentials/prices/results.
26. **Publish SAT Math page and one discovery link.** Add its contextual link from test prep as part of the smallest complete publishable slice. Gate: non-orphan 200 page, unique metadata, self-canonical, sitemap entry, working CTA; complete Google gates below.
27. **Add homepage SAT Math link.** After destination is live, add a useful contextual link. Gate: descriptive anchor with correct destination and no layout regression.
28. **Draft ACT page.** Proposed `/act-tutor-online/`. Verify current exam information against ACT's own sources; describe actual offered services. Gate: useful distinct content, no repeated SAT page with words swapped.
29. **Publish ACT page and one discovery link.** Repeat increment 26's gates for ACT. Update homepage ACT link in a separate small increment after publication.
30. **Draft tutoring-cost guide.** Proposed `/guides/sat-tutoring-cost/`. Use verified Cassidy pricing or clearly described pricing process; source and date any market comparisons. Gate: answers a buying question without unsupported price estimates.
31. **Publish cost guide and one discovery link.** Verify the chosen Hugo content type renders full article body and appropriate metadata, breadcrumbs, author and dates. Repeat Google gates. Add service/booking links naturally.
32. **Draft and publish tutor-vs-class-vs-self-study guide in two increments.** Use a distinct brief and original advice, then the same publication gates. Avoid unsupported “best tutor” claims.
33. **Reassess before adding another SAT service page.** Do not automatically publish the old plan's one-on-one SAT page. Compare actual query/page overlap; expand the existing hub if another page would compete for identical intent.

### Secondary improvements, driven by evidence

34. **Measure mobile performance once.** Record PageSpeed lab results and available Search Console/CrUX field evidence for homepage and one service page. Missing field data on a small site is not failure. Fix only measured issues, one increment per cause, using existing Hugo image sizing/fingerprinting tools. Compare before/after under consistent conditions.
35. **Prepare one legitimate referral opportunity at a time.** Identify relevant education/community resource pages or partnerships that could help families discover Cassidy. Draft outreach separately; do not send messages without authorization, buy links, fabricate city pages, or create a local business listing for an ineligible online-only service.

## Verification gates for every release

| Gate | Exact evidence | What it establishes |
| --- | --- | --- |
| A: Local implementation | Diff plus successful production-mode build with pinned Hugo; rendered HTML and affected links inspected | Source produces intended output |
| B: Live | Deployed commit/build ID, timestamp, HTTP response/redirect chain, actual production HTML containing changed text/metadata | Correct release serves on the public custom domain |
| C: Google access | Search Console Test Live URL; successful fetch, crawl/index permission, tested rendered HTML containing change | Google's inspection system can fetch the current version |
| D: Indexed update | Indexed URL Inspection report, expected Google-selected canonical, last crawl after deployment, changed crawled HTML where available | Google has processed the intended canonical/version; otherwise record uncertainty |
| E: Search visibility | Search Console Performance, exact page plus relevant query/theme filters, dated impressions/clicks | URL is actually being served for relevant searches |
| F: Business response | GA4 organic sessions reaching booking page; verified leads and actual Calendly bookings/qualified inquiries | Traffic is producing interest or bookings |

For B: test homepage and representative service/booking pages after any shared-template change. Check one title, one description, one intended canonical, correct robots directives, parsed JSON-LD, working assets and functional navigation. Verify HTTP/HTTPS and www/non-www settle on the preferred domain without loops. Keep preview deployments excluded from indexing without leaking preview noindex into production.

For C: open Search Console, select the correct property, inspect the exact HTTPS canonical URL, choose Test Live URL, then View Tested Page. Save the fetch result and the changed content/metadata from HTML; inspect the screenshot when layout/rendering matters. Live tests do not prove indexing. [URL Inspection documentation](https://support.google.com/webmasters/answer/9012289).

Submit `https://cassidyartz.com/sitemap.xml` if missing; otherwise check its status and last-read date. A successful read establishes sitemap access, not indexing. Request indexing once per important newly published or materially changed URL after B/C pass, subject to quota. Repeated requests do not expedite crawling. [Sitemap guidance](https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap).

For D: return to the indexed report, not the live-test result. Record status, last crawl, user canonical and Google canonical. If indexed before deployment but not recrawled afterward, status is “indexed, update pending.” If crawled HTML is unavailable, do not claim exact copy adoption from status alone. Redirected and intentionally noindexed URLs have different intended outcomes; their exclusion can be success.

## Expected query-to-page mapping and Google result checks

| URL | Intended search intent / example queries | Desired observation |
| --- | --- | --- |
| `/` | Cassidy Artz; Cassidy Artz tutoring | Brand result leads to homepage with coherent title |
| `/test-prep/` | online SAT tutor; private SAT tutoring; SAT ACT tutoring online | Relevant nonbrand impressions for the main service hub |
| `/sat-math-tutor-online/` | online SAT math tutor; SAT math tutoring | Math-intent queries lead to math page |
| `/act-tutor-online/` | online ACT tutor; private ACT tutoring | ACT-specific queries lead to ACT page |
| `/college-admissions/` | Cassidy Artz college admissions; online college admissions coaching | Admissions-intent visibility |
| `/guides/sat-tutoring-cost/` | SAT tutoring cost; how much does SAT tutoring cost | Cost-research visibility leading toward services |

These are hypotheses, not promised rankings or exact-match requirements. In Search Console Performance select Web, an exact page, a complete date range, consistent country/device, then inspect Queries. Record relevant impressions, clicks, CTR and average position; split branded/nonbranded terms. Query tables can omit low-volume/anonymized data. Zero reported query rows do not prove absence from the index. [Performance report](https://support.google.com/webmasters/answer/7576553).

Manually inspect a few natural Google queries in a signed-out browser, recording date, country/location and device. Check destination and whether title/snippet accurately describes the page. Google may rewrite titles/snippets; exact wording is not an acceptance criterion. Do not repeatedly click your own results. Use `site:` only as a supplemental spot check: results are incomplete and unsuitable as the authoritative index count. [Title links](https://developers.google.com/search/docs/appearance/title-link), [site operator limits](https://developers.google.com/search/docs/monitor-debug/search-operators/all-search-site).

## Observation schedule and next actions

- **Release day:** gates A/B/C, sitemap status, indexing request, analytics smoke test. Record pending D/E explicitly.
- **Days 3–7:** check indexed version/canonical and crawl date once; no repeated submission loop.
- **Days 14 and 28:** reassess unresolved indexing; inspect Performance for intended query themes. Dates are review checkpoints, not indexing deadlines.
- **Days 28/56/90:** compare complete 28-day periods and, where available, comparable prior-year periods because test-prep demand is seasonal. Retain raw counts; low traffic cannot support confident causal claims from percentage changes.
- **Live fetch fails:** resolve HTTP/robots/noindex/rendering problem before content expansion on that URL.
- **Discovered, not indexed:** verify internal discovery links, sitemap, availability and uniqueness; allow crawl time.
- **Crawled, not indexed:** examine useful content, duplication and canonical selection; do not simply resubmit daily.
- **Wrong canonical:** align redirects, internal links, canonical and sitemap; inspect both URLs after recrawl.
- **Indexed, no relevant impressions:** reassess demand, distinct intent, competition and specificity; indexing alone is not SEO success.
- **Impressions but low clicks:** compare query intent, position, competing results and title/description; test one change at a time.
- **Clicks but few booking-page visits:** improve service clarity/proof/CTA and mobile usability.
- **Booking-page visits but few bookings:** verify calendar availability, embed usability and offer expectations; reconcile actual Calendly bookings with GA4 before diagnosing conversion failure.

Do not start recurring automation unless separately requested. The implementing chat should leave dated follow-up checkpoints for the owner if later Google observations cannot happen in that session.

## Evidence record and handoff completion

Maintain one row per URL/release in a separate implementation evidence file:

`increment | URL | intended intent/index status | commit | deploy ID/time | live check/time | sitemap status/read time | live inspection evidence | indexed status/crawl time | Google canonical | indexing request time | query filters/period | impressions/clicks/CTR/position | booking-interest/lead counts | next review | owner/blocker`

Use explicit states: `not started`, `locally verified`, `live verified`, `Google access verified`, `indexed update verified`, `relevant impressions observed`, `business response observed`, or `pending/blocked with reason`. Never prepopulate successful observations.

Suggested first release: increments 1–3, then 10–15; measurement repairs 4–9 can proceed in parallel. Follow with reproduced technical defects, content depth, then one new service page. Before editing heavily overlapping files, coordinate or work sequentially.

For the next chat: implement this plan in order of dependencies, use the Hugo skill, preserve user changes, record evidence after each increment, and resolve implementation defects discovered in testing. Establish deployment authorization from that chat's request before publishing. Report implemented/live/indexed/performing as separate outcomes. Stop for unavailable business facts only where needed, and leave Google-dependent observations pending honestly. Do not declare completion solely because a build passed or a sitemap was submitted.
