# SEO implementation evidence

## September 22, 2026 — first homepage batch

Reference: `seo-implementation-handoff.md`, increments 1–3 and 10–15.

### Baseline

- Branch: `codex/plan-hugo-deck-redesign`; baseline HEAD: `7b5ac8e` (`Use college logo assets in acceptance grid`).
- Existing changes before this batch: modified `hugo_stats.json`; untracked handoff plan and funnel-tracking hook. Preserved. The funnel hook is not yet a verified conversion implementation.
- No AGENTS.md found by repository file search.
- Local Hugo matches Netlify pin: 0.136.5 extended. Production Netlify command invokes Hugo and Pagefind; production deployment ID/commit not verified.
- Hugo Blox v0.3.1 inherited `functions/get_page_title.html` replaces `{brand}` with the entire site title. A literal homepage SEO title avoids changing inner-page titles.
- Inherited `site_head.html` takes descriptions from `summary`, then abstract/page summary/site SEO description. It does not consume the homepage's `seo.description`. Use `summary` for both description and Open Graph description.
- Canonical URLs come from `.Permalink`; robots.txt allows crawling and references the absolute sitemap. Static redirects normalize HTTP and www to HTTPS cassidyartz.com.
- Windsor verified connected GA4 property `519266953` / `CassidyArtz.com`. Connected-source listing returned no Search Console account. No Search Console indexing/performance baseline was obtained; these values remain unavailable.

### Implemented increments

| Increment | Scope | Local evidence | External state |
| --- | --- | --- | --- |
| 10 | Homepage title | Exactly one `Online SAT & ACT Tutoring | Cassidy Artz` title | Deployment/indexing pending |
| 11 | Homepage description | `summary` produces one accurate description and social description | Deployment/indexing pending |
| 12 | Homepage H1 | `One-on-One Online SAT & ACT Tutoring` rendered visibly in browser | Deployment/indexing pending |
| 13 | SAT and ACT links | Both service headings link to `/test-prep/`; destination built | Deployment/indexing pending |
| 14 | Admissions link | Service heading links to `/college-admissions/`; destination built | Deployment/indexing pending |
| 15 | Testimonials discovery | `Read more student success stories` links to `/testimonials/`; destination built | Deployment/indexing pending |

Added underlines and visible keyboard-focus styling to the new text links. Only homepage content/data/template/CSS changed in this batch; no redirects, sitemap exclusions or shared head overrides were introduced.

### Verification

- Before/after production Hugo builds both passed (24 pages, pinned version). Build output and generated resources were directed to `/private/tmp/cassidy-seo-c18ral/`; build statistics writing disabled. No garbage collection used.
- HTML assertions passed: homepage title, description, H1, all four discovery links and built targets, production canonical. Titles/descriptions/canonicals on test prep, admissions, testimonials and schedule matched baseline.
- Pagefind v1.5.2 completed: 12 indexed pages, 695 words. Existing `--source` option is deprecated; this is a warning, not a failure. The repository does not pin Pagefind; this successful local run is not evidence of a deployed Netlify build.
- In-app browser at `http://127.0.0.1:1314/` showed the new title/H1 and links; narrow viewport screenshot showed readable heading and intact booking card.
- `git diff --check` passed.
- This batch has not been committed, published, submitted for indexing, or observed in Google results.

### Preliminary URL disposition (generated sitemap, not authenticated Google evidence)

| URLs | Proposed treatment | Remaining verification |
| --- | --- | --- |
| `/`, `/test-prep/`, `/college-admissions/`, `/testimonials/` | Index | Live HTTP, Google canonical/index status, query baseline |
| `/experience/` | Retain/index if substantive proof | Review usefulness and live index state |
| `/services/testprep/`, `/services/collegeadmissions/` | Investigate consolidation into corresponding main service pages | Confirm live redirects/content/backlinks and Search Console history |
| `/schedule/`, `/lead-generation/` | Retain functional booking; investigate one canonical route | Compare live booking behavior before redirect |
| `/confirmation/` | Proposed noindex plus sitemap exclusion | Implement independently; ensure crawl permitted |
| `/services/`, `/tags/`, `/publication_types/` | Review individually | Determine content value before exclusions |

### Next gates

1. Review this homepage diff and authorize publication when ready; record exact published commit and Netlify deploy ID/time.
2. Fetch production HTML and verify the six changes above, status codes, and production canonical. The localhost preview is not deployment evidence.
3. Obtain Search Console property access. Capture pre-release baseline if still possible. Run Test Live URL for homepage, inspect rendered HTML, and request indexing once after successful checks.
4. Record indexed report/crawl date/canonical at days 3–7 and 14; retain “update pending” until evidence shows recrawl. At day 28, compare page/query impressions and clicks against baseline.
5. Continue measurement repairs (4–9) and reproduced technical defects as independent small changes. A direct confirmation visit must not count as a lead; real iframe event delivery and GA4 receipt still need verification.

## September 22, 2026 — measurement and technical release candidate

### Repository and public baseline

- Repository branch remains `codex/plan-hugo-deck-redesign`; source baseline remains `7b5ac8e`. Existing homepage edits, `hugo_stats.json`, and the unverified funnel hook were preserved.
- Hugo is `0.136.5` extended, matching `netlify.toml`. Netlify production still invokes `hugo --gc --minify -b $URL` followed by Pagefind; no deployment was performed and no deploy ID/commit was available.
- Public `https://cassidyartz.com/` was inspected in the in-app browser on September 22. It still serves the old title `SAT/ACT Tutoring & College Admissions | Cassidy Artz Tutoring | SAT/ACT & College Admissions`, the old Ivy League headline, no homepage service-description links, and no funnel hook. Public canonical is `https://cassidyartz.com/`.
- Public `/schedule/` returns the Calendly iframe with source `https://calendly.com/cassidyartz/lead-generation` and origin `https://calendly.com`; the public page did not contain `booking_page_view` tracking. Public deployment therefore remains pending for every local change in this release candidate.
- No authenticated Search Console property, access role, performance baseline, URL Inspection result, or Google-selected canonical was available. These are unavailable, not zero.

### Implemented increments in this release candidate

| Increment | Scope | Local evidence | External state / next gate |
| --- | --- | --- | --- |
| 4–5 | Booking-page event remains limited to `/schedule/` and `/lead-generation/`; removed the confirmation-page `generate_lead` fallback and invented `$1 USD` value. | Pinned production build passed. In-app browser visit to local `/confirmation/` showed `robots=noindex` and an empty event `dataLayer`; generated confirmation HTML contains no `confirmation_page` conversion source. | Deploy and verify one `booking_page_view` per booking-page load plus GA4 receipt; public hook is currently absent. |
| 6 | Calendly iframe source/origin validation. | Local and public browser inspection both showed the actual iframe source/origin. Listener only accepts messages from `https://calendly.com`; no authorized appointment was submitted, and no real Calendly event delivery was claimed. | Pending: observe a genuine non-submitting Calendly event in a loaded embed. |
| 7 | Completed-booking hardening. | Listener now requires the message source to equal an actual rendered Calendly iframe, allowlists `calendly.event_scheduled`, keeps invitee/payload data out of GA4, deduplicates by event URI with in-memory fallback when storage is blocked, and removes confirmation-page inference. | Pending: browser negative tests against wrong origin/source and duplicate messages, then GA4 DebugView and an authorized end-to-end completion if business owner approves. |
| 8 | Stable CTA locations on homepage links. | Rendered local homepage contains `announcement`, `hero`, `process`, `services`, `testimonials`, `closing`, and `footer` location labels; identical booking labels remain normal links to `/schedule/`. | Pending deployment and live click-event verification. |
| 16 | Breadcrumb JSON-LD repair. | Reproduced prior literal wrapping quotes in generated breadcrumbs, then fixed serialization. Hugo 0.136.5 output for `/test-prep/` and `/confirmation/` parses as JSON; names are plain text and item URLs are absolute `https://cassidyartz.com/` URLs. | Pending live HTML and Google Rich Results validation. |
| 17 | Business/entity JSON-LD serialization. | Added a project override that serializes the entity as valid JSON-LD and retains only configured facts: `LocalBusiness`, Cassidy Artz, logo, and URL; no address or coordinates were invented. Local JSON-LD parses. | Pending live HTML and Rich Results validation; schema validity does not establish a rich result. |
| 23 | Confirmation utility-page indexing controls. | Added `private: true` (theme emits `meta name="robots" content="noindex"`) and `sitemap.disable: true`. Generated sitemap omits `/confirmation/`; generated HTML retains crawlable noindex. | Pending deployment and eventual Search Console exclusion for the intended reason. |

### Verification record

- Production-mode Hugo build passed with the pinned `0.136.5` binary: 24 pages, 3 non-page files, 4 static files, 20 processed images. Output was isolated under `/private/tmp/cassidy-seo-release-public2`; generated resources did not replace tracked site output.
- Generated checks passed for homepage title/H1/CTA locations, booking hook source, confirmation noindex/sitemap exclusion, clean breadcrumb JSON-LD, clean business JSON-LD, and production absolute canonical URLs. `git diff --check` passed before the final evidence update.
- In-app browser inspection passed for desktop homepage layout/navigation and local confirmation behavior. A local booking page rendered the iframe with the intended Calendly source; the external Calendly content was not available in the local preview, so event delivery was not asserted. The in-app browser session did not expose a viewport override capability for a separate mobile viewport; mobile visual verification remains outstanding.
- Pagefind production check was attempted with `npx --yes pagefind --version`, but no local Pagefind binary was available and package resolution could not complete in the restricted environment. The complete Netlify Hugo-plus-Pagefind command remains outstanding; this is a verification blocker, not a build failure.

### Content increment

| Increment | Scope | Local evidence | External state / next gate |
| --- | --- | --- | --- |
| 25 | Draft `/sat-math-tutor-online/` using only existing test-prep facts: math/data-analysis topics, calculator use, pacing, diagnostic inputs, online one-on-one format, and existing CTA paths. | Normal production build remains 24 pages and excludes the draft from the sitemap. A `--buildDrafts` build renders 25 pages with unique title, description, self-canonical, answer-first sections, FAQs, and scheduling/test-prep/testimonial links. | Deliberately not published. Cassidy must approve the page facts and provide any approved proof example before increment 26 can publish it and add discovery from `/test-prep/`. |

### State separation and blockers

| Outcome | Current state |
| --- | --- |
| Implemented and locally verified | Homepage batch plus increments 4–8, 16–17, and 23 are implemented in the working tree and locally verified as above. |
| Deployed and verified on public domain | Pending. Public HTML is still the pre-release version. |
| Accessible through Search Console live URL test | Pending; property access is unavailable. |
| Indexed with intended Google canonical and post-deployment crawl | Pending; no authenticated inspection data. |
| Receiving relevant search impressions/clicks | Pending; no Search Console performance data. |
| Producing booking interest and confirmed bookings | Pending; public tracking is not deployed, GA4 receipt was not verified, and no real test booking was submitted. |

Next action: review this release candidate, resolve/authorize the Pagefind verification environment if needed, then approve a production deployment. After deployment, record the exact commit/deploy ID, repeat public metadata/redirect/sitemap checks, run the prescribed Search Console live test and one indexing request per eligible URL, and keep indexing/performance/booking outcomes pending until observed.
