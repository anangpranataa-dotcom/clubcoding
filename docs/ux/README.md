# ApiPantau — UX Deliverables (QA)

Source of truth for the mobile UX contract in M1–M4. Owned by the **QA seat** (`docs/TEAM.md:15`).
Design log: [`design-log/0005-ux-flows-and-design-tokens.md`](../../design-log/0005-ux-flows-and-design-tokens.md)
(`AP-008`).

| | |
|---|---|
| Status | Proposed — awaiting TL approval |
| Task | `AP-008` |
| Owner | QA — Anang |
| Last updated | 2026-11-07 |
| Consumers | MOB-A, MOB-B, BE (copy/state contract), WEB (status vocabulary) |

## What is here

| File | Contents | Implementing tasks |
|---|---|---|
| [`flows/01-report.md`](flows/01-report.md) | Report flow: FAB → photo → review/send, offline queue, permissions, failure states | `AP-020`, `AP-021`, `AP-022`, `AP-025` |
| [`flows/02-map-incident.md`](flows/02-map-incident.md) | Map layers, legend, marker bottom sheet, incident detail, radius 2/5/10 km | `AP-009`, `AP-030`–`AP-033` |
| [`flows/03-alerts.md`](flows/03-alerts.md) | Alert list, notification permission, push content, deep link, preferences, anti-spam | `AP-052`, `AP-053`, `AP-050`–`AP-054` |
| [`flows/04-verify.md`](flows/04-verify.md) | Verifier queue, report detail, `konfirmasi`/`tolak`/`butuh_info`, audit, conflicts | `AP-060`–`AP-062` |
| [`design-tokens.md`](design-tokens.md) | Colour (light/dark), type, spacing, size, radius, motion, contrast table | TL/MOB-A in `core/theme` |
| [`copy-deck.md`](copy-deck.md) | All Indonesian UI strings by ID, status labels, errors, empty states, push copy | All mobile seats |
| [`components.md`](components.md) | Component contracts: buttons, chips, banners, sheets, cards, states | MOB-A, MOB-B |

## Reading order for implementers

1. `design-log/0005-ux-flows-and-design-tokens.md` — decisions and non-negotiables (10 min).
2. The flow you are implementing.
3. `copy-deck.md` + `design-tokens.md` — never invent a string, colour, or spacing value.
4. `components.md` — reuse the shared shapes instead of new widgets.

## Contract rules

1. **Status vocabulary is fixed.** Use the mapping in `copy-deck.md`; never render raw database
   values (`menunggu_verifikasi`) or English SDK text.
2. **One primary action per screen.** Destructive/negative actions require a reason.
3. **No colour-only meaning.** Icon + label + colour together.
4. **Every surface has loading, empty, error, offline, and permission-denied states** where
   applicable. A blank screen is a defect.
5. **Permissions are contextual.** Rationale first, OS prompt second; denial is recoverable.
6. **Accessibility floor:** ≥ 14 sp text, ≥ 48 dp targets, 56 dp primary CTA, AA contrast,
   dark mode.
7. **No new copy outside the copy deck.** Add an ID here first; then implement.

## Boundaries

AP-008 owns **UX specification only**. It does **not** produce:

- Flutter widgets, theme code, routes, or models — MOB-A/MOB-B/TL;
- backend, RLS, RPC, SQL, schema, or seed data — BE;
- admin dashboard screens — WEB;
- test code or test strategy — `AP-027`;
- accessibility audit — `AP-085`;
- UAT script — `AP-088`;
- product naming, platform scope, or release decisions — TL.

If a flow needs a capability outside these documents, raise it as a dependency in the design log
rather than inventing UI.

## Handoff checklist

- [ ] TL approves DL-0005 (`Proposed → Approved`).
- [ ] MOB-A confirms the report flow can be built in 3 actions with `image_picker`.
- [ ] MOB-B confirms marker-sheet content matches `AP-031` and `AP-033` inputs.
- [ ] BE confirms the failure/rate-limit responses needed by the copy deck.
- [ ] QA walks the first build against each flow checklist and files gaps as `AP-1xx`.

## Open dependencies

| Dependency | Owner | Status |
|---|---|---|
| Deep link survives login (`/incident/:id`) | MOB-B, `AP-052` | Open — current router redirects to `/map` |
| Rate-limit response distinguishable from generic 4xx | BE, `AP-026` | Open |
| Offline queue state names/badges | MOB-A, `AP-022` | Open |
| Role claim for hiding Verifikasi | MOB-A/BE, `AP-010` | Open |
| Demo data for non-empty map/list states | BE/WEB, `AP-080` | Open |

## Change control

Edits to these documents are UX changes and follow the design-log rule (`AGENTS.md:34`): update
the spec, note the reason in DL-0005 `## Implementation Results`, and tell the implementing
seat. A new screen or a new status is new scope — raise it with the TL, do not add it silently.
