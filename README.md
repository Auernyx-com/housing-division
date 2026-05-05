# Housing Division

SQUAD Battalion — Housing Division

Veteran housing navigation for Western Slope Colorado (pilot). Deterministic pipeline that takes a veteran's situation and finds the right housing path — cutting through HUD-VASH eligibility rules, HQS inspection requirements, listing scams, and landlord friction.

## Pipeline

Four modules chain together in sequence:

```
Listing
  → Listing_Legitimacy_RedFlags    (is this listing real?)
  → ProgramGate_HUDVASH_HCV_S8    (can the program pay for it?)
  → HQS_PreInspection_Screener    (will it pass inspection?)
  → Landlord_Outreach_Packet      (ready-to-send landlord contact package)
```

## Modules

| Module | What it does |
|---|---|
| `Listing_Legitimacy_RedFlags/` | Scam and red flag detection on rental listings. Risk score 0–100, structured red flags, next steps. |
| `ProgramGate_HUDVASH_HCV_S8/` | Eligibility and affordability gate for HUD-VASH, HCV, and Section 8. Payment standard math, rent cap checks, auto-generates "Ask PHA" questions. |
| `HQS_PreInspection_Screener/` | Pre-screens a unit against HUD Housing Quality Standards before wasting a showing. Catches predictable failures early. |
| `Landlord_Outreach_Packet/` | Takes the three gate outputs and produces a call script, SMS, email, doc checklist, and fix list ready to send to the landlord. |

## Location config

`ProgramGate_HUDVASH_HCV_S8/v1/PHAOverrides_MesaCounty_CO.json` — Mesa County / Grand Junction pilot config.

**Payment standards and utility allowances are PLACEHOLDERS.** Fill from:
- HUD FMR tables: https://www.huduser.gov/portal/datasets/fmr.html (Mesa County, CO)
- Grand Junction Housing Authority: utility allowance schedule

Do not route veterans to housing decisions until those values are populated and verified.

## Part of SQUAD Battalion

This repo is the Housing Division — one module in the SQUAD Battalion swarm. It attaches to the `squad-battalion` coordinator (Pathfinder) the same way SQUAD Battalion attaches to Auernyx Mk2.

Governance, receipts, and audit trail flow through the Mk2 platform.
