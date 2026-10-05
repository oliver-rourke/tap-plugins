# Claude for Record Clearance

A Claude plugin for the people who run record clearance programs: legal aid offices, public defender clean slate programs, law school clinics and reentry nonprofits. Built by [The Access Project](https://accessprojectca.org) in the layout of Anthropic's [Claude for Legal](https://github.com/anthropics/claude-for-legal) plugin suite. Apache 2.0.

Staff paste an intake, or an attorney describes a conviction, and the plugin runs two checks and tells the attorney what to file.

## Two checks

1. **Intake triage.** From the intake answers alone, the routing a mature intake form carries: program gates, prior review decision, pending case, supervision today and in the past three years (with the fire camp exception and the two-year and one-year waits), registration, trafficking or DV, the five consents. Outcomes: proceed to the screen, needs attorney review, not eligible now with a recheck, or not eligible for the program with the referral step.
2. **Eligibility screen.** The facts of each conviction are confirmed as yes-or-no lines, then screened under Penal Code sections 1203.4, 1203.4a and 1203.41, with a flag where PC 1203.425 automatic relief may already have acted, recheck dates with the arithmetic shown, and a filing bullet for the county: the forms (CR-180, CR-181, proof of service, declaration when the route is discretionary), how the prosecutor is served, and one local rule, for all 58 California counties.

What is published here is the statutory decision table, written from the Penal Code text with every rule pinned to its subdivision. The Access Project's engine lists and heuristics are not part of it. Every output is an attorney-review draft; the plugin routes, it does not decide; nothing goes to an applicant without the review model the supervising attorney sets at setup; names, contact details and dates of birth are dropped on the way in.

## Try it in two minutes

**Claude Cowork:** Plugins, Add marketplace, enter `cleanslate-engine/tap-plugins`, then install Record Clearance Legal.

**Claude Code:**

```
/plugin marketplace add cleanslate-engine/tap-plugins
/plugin install record-clearance-legal@tap-plugins
```

Then, as the supervising attorney:

```
/record-clearance-legal:cold-start-interview
```

Pick the quick start (two minutes). Then try three prompts:

```
/record-clearance-legal:eligibility-screen
Misdemeanor PC 484(a), Mono County, convicted 2019. Probation granted and completed with no violations, ended March 2021. Nothing pending, not on any supervision, no 290 registration, no fire camp. Screen it and tell me what we file.
```

```
/record-clearance-legal:eligibility-screen
Nothing pending, not on any supervision now or in the past three years, no 290 registration, no fire camp. RAP entry:
5/23/2023
SAN DIEGO CENTRAL
MISDEMEANOR
11377(A) HS-POSSESS CNTL SUBSTANCE
sentence: 002 YEARS PROBATION
successfully completed
```

```
/record-clearance-legal:intake-import
(paste a form response; the sample in record-clearance-legal/references/sample-intakes/12-parole-waiting-period.md ends at NOT ELIGIBLE NOW with a computed recheck)
```

The first returns LIKELY ELIGIBLE on the PC 1203.4 mandatory route and a "Filing in Mono County" bullet: CR-180, CR-181, CR-106 proof of service by mail, serve the DA by mail. The second maps the RAP lines to San Diego County, estimates the probation end from the term, and lists the county's work-up sheet. Every output is synthetic until you connect your own intake.

## What is in the box

- `record-clearance-legal/` — the plugin: four skills (`cold-start-interview`, `customize`, `intake-import`, `eligibility-screen`), the rulebook, statute cards with dated fetches, the county filing guide, twelve synthetic fixtures with expected results, and a `claude plugin eval` suite of fourteen cases.
- `.claude-plugin/marketplace.json` — makes this repository installable as a marketplace named `tap-plugins`.

The same plugin sits on a branch of [our fork of Claude for Legal](https://github.com/cleanslate-engine/claude-for-legal/tree/record-clearance-legal/record-clearance-legal), in the suite's layout with its marketplace entry and documentation rows, ready for an upstream pull request.

## Connectors

Optional: Typeform and Airtable (read-only intake), CourtListener (citation checks), Slack and Google Drive. Paste and CSV cover every workflow without them.

> **Disclaimer:** Every output is a draft for attorney review, not legal advice, not a legal conclusion, not a substitute for a lawyer. The attorney using the plugin is responsible for the legal positions taken in their work product.
