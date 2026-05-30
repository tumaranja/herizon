# Audit — `match.herizon.io` Option B (router gate)

**Mockup file:** `mockup-option-b-router-gate.html`
**Design direction:** Herizon's actual shadcn dark theme (palette lifted from `match.herizon.io`'s live CSS bundle)
**Date:** 2026-05-30

---

## Direction choice — quick justification

The first pass used a calm/airy + sage palette as a conservative read of "monochrome brand book." After inspecting the live site (`match.herizon.io` ships Next.js + Tailwind + shadcn/ui in dark mode by default), the palette is now lifted verbatim from their CSS bundle:

- `--background: #0a0a0a` (near-black)
- `--foreground: #fafafa` (off-white)
- `--card: #111`, `--muted: #1a1a1a`, `--border: #262626`
- **`--primary: #a78bfa`** (violet — the "bright purple Continue with email" CTA from the prior session)
- `--muted-foreground: #a0a0a0`
- Inter font (already loaded by the live site), `rounded-md` (6px) buttons, `rounded-xl` (12px) cards

The mockup reads as a Herizon page, not a separate aesthetic. Differentiation from `join.herizon.io` therefore lives in:

- **Density and rhythm.** Denser proof + pricing sections, mono-typed eyebrows and labels, sharper section transitions — signals "tool for serious buyers" without breaking the brand palette.
- **The gate itself.** Two equal-weight tiles, generous whitespace, no form. Different *structure*, same *language*.
- **Copy tone.** Buyer-language throughout ("Post my first role", "Continue as a company") vs. the warmer talent-side framing on `join.`.

All tokens are in `:root` CSS custom properties — if the brand book demands a different accent or a stricter neutral, it's a one-line swap.

---

## Deviations from the locked IA

One deliberate deviation, plus structural notes:

1. **Inserted "Section 0: Gate" before the Header.** The whole Option B move. Full viewport, no form, two equal-weight tiles. This is the **only** addition above the locked IA — everything below the gate sits in its standard order.
2. **Header is sticky-on-scroll-past-gate** (not always-visible). Until a visitor self-selects, the page reads as a router, not a product landing. After self-select, the header materializes with the primary CTA.
3. **Hero stats row replaces a logo bar.** Client has real numbers (50+ companies, 250+ matches) but no permission-granted logos in materials supplied. Using numbers is more honest than fabricated logos.
4. **Founder section is kept but heavily `MISSING`.** Herizon is a Finnish non-profit (Reg. no. 3277100-2) — that's a high-credibility signal. Kept the section as a placeholder skeleton so the gap is visible to the client.

---

## Part 1 — 5-second test (the gate)

1. **First impression** — "This is a router, not a product page." Two equal tiles, no form, minimal chrome. Good.
2. **Feeling** — Deliberate, quiet, slightly editorial. Not warm. Trustworthy in a B2B way.
3. **What stands out** — The two tile titles ("I'm hiring talent" / "I'm looking for work") draw the eye first. Correct — that's the action.
4. **Brand clarity** — "Herizon · Talent Matcher" wordmark top-left is clear. The sub-label "match.herizon.io" top-right anchors which subdomain you're on.
5. **Credibility** — Sufficient for a router. No proof on the gate intentionally — proof lives below, after self-selection, where companies will actually read it.
6. **Who is it for** — Both sides. That's the point. The 5-second answer is "pick your side", not "this is for X."

**5-second test of the below-gate hero** (run separately because companies scroll past the gate):

1. **First impression** — "Employer landing for a Finnish hiring platform with real traction."
2. **Feeling** — Calm and credible. Less warm than `join.`, which is correct.
3. **What stands out** — The H1 "Hire diverse, pre-vetted talent." Eye then jumps to the 4 stats row.
4. **Brand clarity** — Yes.
5. **Credibility** — Stats row carries it. Once `MISSING` quote / logo content lands, this gets stronger.
6. **Who is it for** — Companies hiring in Finland & the EU. Eyebrow says it explicitly.

---

## Part 2 — Detailed analysis

1. **Logical order.** Gate → Hero → Problem → How → Use cases → Proof → Founder → Objections → Pricing → Final CTA. Standard locked IA below the gate. Gate is the deliberate deviation. Logical.

2. **Structure within sections.** Sections use a consistent "eyebrow (mono caps) → H2 → lede → content" rhythm. Coherent.

3. **Confusion points.**
   - Gate eyebrow reads *"A two-sided platform — pick your side to continue"*. "Pick your side" is faintly competitive ("which side are you on?") — fine, but if the client wants warmer, swap to *"Choose the experience that fits you"* or similar.
   - Hero subhead crams 4 facts into one sentence (post for free, AI matching, €1,500 + VAT, interns free). Skimmable but dense.
   - **The gate appears to "block" a returning company who just wants to log in.** No "Already have an account?" affordance on the gate. Flag this — if the live site uses match.herizon.io as both login and signup entry, the gate needs a small "Log in" link in the header area.

4. **Unanswered questions a real visitor would still have.**
   - "How does AI matching actually work?" — no explanation deeper than the step.
   - "Who's already hired through this?" — answered only by stats and `MISSING:` quotes.
   - "What's the catch on €0 internships?" — pricing card mentions it but doesn't address suspicion.
   - "Is this only for tech roles?" — use cases hint, but no explicit answer.

5. **Clear next step.** Yes, at every scroll position. Above gate: tiles. Sticky header (post-gate): "Post my first role" button. End: final CTA. Pricing cards do **not** have their own CTA buttons — intentional (one repeated CTA, not per-tier inflation), but worth mentioning if the client expects per-tier buttons.

6. **Things to add.**
   - A small **"Already have an account? Log in →"** link on the gate header (right side, near `match.herizon.io` label). Doesn't compete with tiles. Removes the login-trap.
   - **OG image / meta** for the page — the prior session called out organic-social traffic as the source of wrong-doors. The mockup is just the page; the social preview card needs its own fix outside this file.

7. **Things to rearrange.** Nothing structural. One micro-fix: the founder section currently sits between Proof and Objections (correct per locked IA) but tonally it's the warmest section on the page. That's actually right — the locked IA reasoning explicitly says warmth here is the point.

8. **UX issues.**
   - **The tile click region is the entire card** (anchor wraps the card). Good for big-target accessibility.
   - **Keyboard tab order** lands gate-header wordmark → gate hiring tile → gate talent tile → footer link. Clean.
   - **Mobile gate** collapses tiles to one column — tested mentally, no overflow.
   - **The email-block message uses `role="alert"` + `aria-live="polite"`** — screen-readers will announce it.

9. **Bugs / tech issues.**
   - Sticky header `backdrop-filter` is OK on Safari/Chrome; fallback is the solid `rgba(250,250,247,0.92)` color — readable.
   - `text-wrap: balance` and `pretty` baked in per skill spec.
   - All visible quotes use curly `" "` (verified manually).
   - No `<img>` tags used — all visuals are CSS-rendered or placeholders. Means the page works with no assets pipeline.

---

## Part 3 — ResearchXL scoring per section

A 5 is rare — best-in-class for the category. A 3 means "fine but a competitor could match this." Score ≤3 gets a concrete fix.

### Gate (added section)

- **Clarity: 5** — H1 names the choice ("Are you hiring, or looking for work?"), tiles are labeled, action verbs on each.
- **Relevance: 5** — for an organic-social-traffic mix that's 40% wrong-door, this directly addresses the wrong-door at the door.
- **Value: 4** — tile descriptions name what the visitor gets ("Post a role" / "Apply via Herizon"). Could be sharper on the talent side ("Free courses, AI tools..." is correct from `join.` materials).
- **Friction: 5** — one click to route. No form, no scroll required.
- **Distraction: 5** — there is literally nothing else on the gate above the fold. Whole point of the section.
- **Anxiety: 4** — "match.herizon.io" sub-label top-right anchors context. **Fix:** add small "Already a customer? Log in →" affordance on the gate header (right area) — current absence creates an anxiety point for returning users.
- **Motivation: 4** — eyebrow + H1 are clear. The talent-side tile may actually pull undecided visitors to `join.` faster than they'd self-select on the current page. That's a win for both sides.
- **Buying-stage match: 5** — early-research and decision-stage visitors both benefit. The decision-stage company clicks once and is in the funnel.

### Header (sticky, post-gate)

- **Clarity: 4** — Logo + back-to-gate + primary CTA. Read in one beat.
- **Relevance: 5** — Sticky CTA is "Post my first role" — buyer-frame.
- **Value: 4** — CTA could be even tighter, e.g. "Post a role in 10 minutes" — but length tradeoff.
- **Friction: 5** — no nav menu, no distraction.
- **Distraction: 4** — the "← Not hiring?" ghost link is a deliberate route-out; small enough not to compete.
- **Anxiety: 5**.
- **Motivation: 4**.
- **Buying-stage match: 5**.

### Hero

- **Clarity: 5** — H1 in buyer language ("Hire diverse, pre-vetted talent"). Echoes the client's own copy.
- **Relevance: 5** — Eyebrow "For companies hiring in Finland & the EU" message-matches the implied search/social intent.
- **Value: 4** — Subhead packs free posting + €1,500 + intern-free + AI matching. Dense. **Fix:** consider splitting into a short subhead + a single-line proof strip beneath: *"Subhead: Get matched with international professionals from the Herizon community."* + *"Strip: Free to post · €1,500 + VAT per hire · Internships free."*
- **Friction: 4** — Form is one field. **Fix candidate:** add inline domain hint (live as the user types — "looks like a personal email") rather than only on submit. Mockup currently only validates on submit.
- **Distraction: 4** — Secondary CTA ("see how it works") was dropped in favor of the inline form. Defensible — one primary action, repeated.
- **Anxiety: 3** — Stats are credible but there are zero named customer logos visible. **Fix:** as soon as 3+ named-permission logos exist, add a row directly below the form with text "Hiring teams already on Matcher:" + logos. Until then, stats hold but it's thin.
- **Motivation: 5** — outcome-anchored.
- **Buying-stage match: 5**.

### Problem

- **Clarity: 4** — three concrete pain bullets in buyer language.
- **Relevance: 4** — speaks to small-team Finnish hiring managers. May not resonate as strongly for larger TA teams — but the use cases section already implies SMB scale.
- **Value: 4** — every bullet is specific (sourcing, vetting, pay-and-pray).
- **Friction: 5** — passive read.
- **Distraction: 5**.
- **Anxiety: 4** — naming pain reduces anxiety by signaling understanding.
- **Motivation: 4**.
- **Buying-stage match: 4** — early-evaluation, less useful for decision-stage.

### How it works

- **Clarity: 5** — 3 steps, ≤2 sentences each, ordered.
- **Relevance: 5**.
- **Value: 4** — Step 3 names the price moment ("€1,500 + VAT only when someone signs") — anchors trust mid-funnel.
- **Friction: 5**.
- **Distraction: 5**.
- **Anxiety: 4** — "First role posted in under 10 minutes" + "First matches typically within 48 hours" are the time-to-value signals. **Verify with client** — if 48 hours isn't real, change the lede.
- **Motivation: 5**.
- **Buying-stage match: 5**.

### Use cases

- **Clarity: 3** — three buckets (software/data, product/design, internships) but two are `MISSING:` for outcome metrics. **Fix:** as soon as the client supplies real role-mix from 90 days of product data, replace the categories + the outcome lines. Until then, this section reads as skeleton.
- **Relevance: 4** — covers the obvious buckets but Finnish hiring is broader.
- **Value: 3** — outcomes are placeholders. **Fix:** see above.
- **Friction: 5**.
- **Distraction: 5**.
- **Anxiety: 4** — internship card is concrete ("20+ interns placed").
- **Motivation: 3** — without numbers, the "want this for my team" reaction is weaker. **Fix:** numbers per card.
- **Buying-stage match: 4**.

### Proof

- **Clarity: 3** — section reads as scaffolding because the entire quote area is `MISSING:`. Real quotes will lift this immediately.
- **Relevance: 5** when populated.
- **Value: 2** — currently no value because no real quotes. **Fix (top priority):** 1 strong hiring-manager quote with name/role/company; 2 secondary quotes (one company side, one intern-host side).
- **Friction: 5**.
- **Distraction: 5**.
- **Anxiety: 2** — proof is the anxiety section. Empty = weak. **Fix:** same as Value.
- **Motivation: 3**.
- **Buying-stage match: 4**.

### Founder

- **Clarity: 4** — Layout is right (compact, photo + 1-2 line quote + name/role). Content is `MISSING:`.
- **Relevance: 5** — Finnish non-profit, founder-led, employer-funded model is a real trust lever.
- **Value: 4** when populated. Currently `MISSING:`.
- **Friction: 5**.
- **Distraction: 5**.
- **Anxiety: 2** when empty. **Fix (top priority):** founder photo + 1–2 line belief-driven quote. This is the single highest-leverage missing asset on the page given Herizon's non-profit positioning.
- **Motivation: 4** when populated.
- **Buying-stage match: 5**.

### Objections

- **Clarity: 3** — Three FAQ items, but all three answers are `MISSING:`. The objection *questions* are guesses (vetting, no-good-applicants, work permits) — directionally right but need real top-3 from sales calls.
- **Relevance: 4** if the guessed questions match the real top 3.
- **Value: 2** — no answers yet. **Fix:** real objections + real answers from a hiring-manager sales call.
- **Friction: 5**.
- **Distraction: 5**.
- **Anxiety: 2** — empty answers = anxiety unaddressed. **Fix:** see Value.
- **Motivation: 3**.
- **Buying-stage match: 5** — objections always serve decision-stage.

### Pricing

- **Clarity: 5** — €0 interns + €1,500/hire for paid roles. Two cards, clear.
- **Relevance: 5**.
- **Value: 5** — transparent pricing is a strong trust signal per Verna.
- **Friction: 4** — no CTA per card (one repeated CTA elsewhere). Defensible. **Verify with client** if they want a per-card CTA.
- **Distraction: 5**.
- **Anxiety: 4** — "Pay only when an offer is signed" line addresses the obvious "what if no one good applies" anxiety. The Objections section needs to back this up with a refund / re-match policy.
- **Motivation: 5**.
- **Buying-stage match: 5**.

### Final CTA

- **Clarity: 5** — Headline restates the activation ("Post your first role in under 10 minutes").
- **Relevance: 5**.
- **Value: 5** — time-to-value + free posting reaffirmed.
- **Friction: 5**.
- **Distraction: 4** — secondary "Looking for work →" link is intentional final-route-out for any wrong-door who scrolled this far.
- **Anxiety: 5**.
- **Motivation: 5**.
- **Buying-stage match: 5**.

---

## Part 4 — Conversion equation pass

`C = 4m + 3v + 2(i - f) - 2a`

- **m (motivation match): 4** — Gate matches the dual-audience reality of the inbound mix. Hero (post-gate) matches buyer intent. Drops to 3 only for visitors who searched for a *specific* role-type and expected a job-board-style landing.
- **v (value clarity): 4** — Headline + stats + 3-step + transparent pricing carry value. Drops because `Proof`, `Objections`, and `Founder` are placeholders. Once populated → 5.
- **i (incentive to act now): 3** — "Free to post" + "first matches in 48 hours" are present but soft. **Fix:** add a small live indicator if real ("3 hiring managers posted in the last 24 hours" — only if true; do not invent). Or a Q3 hiring-window framing tied to seasonal demand.
- **f (friction): 4** — One email field. Domain block adds friction *for the wrong audience* (correct per CXL "strategic friction" play). 5 once login affordance is added.
- **a (anxiety): 3** — Stats + pricing transparency hold. Anxiety is high because Proof / Founder / Objections are placeholders. **Fix:** populate those three sections — single biggest lever.

Highest-leverage fix: **`a`** — populate Proof, Founder, and Objections with real content. Single biggest swing.

---

## Part 5 — Final recommendation

### Top 3 fixes, ranked by impact

1. **Populate Proof, Founder, and Objections with real content.** This is the single biggest swing on the conversion equation (anxiety). Without these three sections, the mockup leans on the gate + pricing transparency alone. With them, the page becomes load-bearing. Specifically: one strong hiring-manager quote with name/role/company; founder photo + 1–2 line belief quote; real top-3 objections from sales calls with direct answers. See "Content gaps for v2" below.

2. **Add an "Already have an account? Log in →" affordance on the gate header (right side).** The gate currently has no path for returning users. If `match.herizon.io` is the login entry too, this is a real bug — returning customers will bounce. Suggested placement: replace the "match.herizon.io" sub-label top-right with `[Log in →]` as a small ghost link, or add it as a second item. Costs nothing, removes a real friction point.

3. **Split the hero subhead.** It currently crams four facts into one sentence (free to post + AI matching + €1,500 per hire + interns free). Split into: a clean one-line subhead ("Get matched with international professionals from the Herizon community.") + a single-line proof strip beneath ("Free to post · €1,500 + VAT per hire · Internships free."). Easier to skim, same density.

### Content gaps for v2 — what to extract from the client next

Specific asks, in priority order:

1. **One strong hiring-manager quote** with permission to publish name + role + company. Should reference a specific role they filled and a time-saved or shortlist-quality outcome.
2. **Two secondary quotes** — one from a company side (different role type), one from an intern host (lean into the UAS partnership angle).
3. **Founder photo** — expressive, in-workspace, NOT a LinkedIn headshot. Plus a 1–2 line founder quote on why Herizon exists and why now. Belief-driven, not feature-driven. Founder name + LinkedIn URL.
4. **Real top 3 objections from sales calls.** The three guessed in the mockup (vetting process / "what if no one good applies" / work permits) are directionally right but need verification. Each objection needs a real, direct answer — including the awkward ones (refund policy? re-match? sponsorship?).
5. **Use-case data from product** — real role-mix from the last 90 days. Replace the three guessed categories (software/data, product/design, internships) with the actual top 3 categories companies posted. Include numbers: average time-to-shortlist or time-to-hire per category.
6. **3–5 named company logos with permission.** Adds to hero credibility row + use cases. Without these, the stats row carries credibility alone.
7. **Confirm the "first matches within 48 hours" claim** — if not true, replace with the real number. If higher, frame around it ("First shortlist within 5 business days" still works).
8. **OG / social share image** — this is outside the HTML but the original problem (organic-social traffic) starts at the link preview card, not the page. Brief asset request: a card image that visually leans "for employers" so the wrong-door starts before the click.
9. **Brand book** — would let me lock the accent more confidently. Currently using a quiet sage `#2D4A2F`. If the brand has an actual accent or a stricter palette restriction, swap is a one-line CSS change in `:root`.

---

## "Would I be embarrassed?" check

Three things I'd want fixed before this lands in front of the client without explanation:

1. **The Proof section reads as scaffolding.** `MISSING:` placeholders are the right convention per skill rules, but a client glancing at this page might mistake it for skeleton content. Mitigation: lead the meeting with the wireframe page (`wireframe-annotated.html`), then show the mockup with the placeholders explicitly framed as "these are deliberate gaps — they're what we'd ask you for next."

2. **The gate eyebrow phrasing.** *"A two-sided platform — pick your side to continue"* — "pick your side" is faintly adversarial. If the brand wants warmer, swap to "Choose the experience that fits you" or "Which side are you on today?". Trivial fix.

3. **No login affordance on the gate.** Real bug for returning customers. Top 3 fix #2.

Everything else passes the gut-check.
