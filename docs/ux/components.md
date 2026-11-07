# Component Contracts

| | |
|---|---|
| Task | `AP-008` |
| Owner | QA — Anang |
| Implementers | MOB-A / MOB-B; shared widgets under `core/widgets` (TL review) |
| Design log | DL-0005 |
| Status | Proposed |

Reusable shapes that keep the four flows consistent. Values come from
[`design-tokens.md`](design-tokens.md); strings come from [`copy-deck.md`](copy-deck.md). This
file defines behaviour and anatomy, not Dart classes.

## 1. Buttons

| Variant | Height | Fill / border | Label | Use |
|---|---|---|---|---|
| Primary | 56 dp | `primary` / none | `onPrimary`, 14 sp 600 | One per screen: Kirim laporan, Konfirmasi laporan, Aktifkan notifikasi |
| Secondary | 48 dp min | transparent / 1 dp `outline` | `primary` | Alternative path: Pilih dari galeri, Butuh info |
| Text | 48 dp | none | `primary` | Low-emphasis: Nanti saja, Buka Pengaturan |
| Destructive text | 48 dp | none | `error` | Tolak, Buang |
| Destructive filled | 56 dp | `error` / none | `onError` | Only inside a confirmation dialog |
| Icon | 48 dp | optional tonal | `onSurfaceVariant` | Back, close, layers, locate |
| FAB | 56 dp | `primaryContainer` or `primary` | `onPrimaryContainer` / `onPrimary` | **Lapor** only |

Rules:

- Full-width primary inside forms and sheets; inline primary in dialogs.
- Disabled: 38% content, no elevation, no pressed state; the reason for disabling is stated
  nearby when it is not obvious.
- Pressed overlay 12% for 120 ms; no ripple on map markers.
- Loading state replaces the label with **Mengirim…** / **Menyiapkan foto…** and a small
  progress indicator; width does not jump.
- Every button exposes a semantic label; icon-only buttons require a tooltip.
- Never use colour alone for destructive intent: the label says "Tolak laporan".

## 2. Text fields

- Height 56 dp single-line; multiline grows to 4 lines then scrolls.
- Label above the field (not only placeholder); helper text below; error text replaces helper in
  `error` tone and is announced to screen readers.
- Counter appears at 240/280 for notes and reasons.
- Reason fields (`tolak`, `butuh_info`) open with focus and keyboard; CTA stays disabled until
  10 characters.
- `maxLength` is enforced, not truncated silently.
- No inline validation before the first submit attempt.

## 3. Selection controls

**Segmented control** (radius 2/5/10 km)

- Three equal segments, 48 dp high, 12 dp radius; selected = `primaryContainer` +
  `onPrimaryContainer` + check icon; unselected = transparent + `outline`.
- Selection saves immediately; no "Apply" button.
- Entire segment is tappable, not just the label.

**Switch row**

- Whole row 48 dp high toggles; label left, switch right; helper text below when needed.
- Locked row: switch disabled, label and helper stay at full contrast; a lock icon explains why.
- Toggling shows the new state immediately; on failure revert and show the failure string.

## 4. Chips and badges

| Chip | Height | Content | Interactive |
|---|---|---|---|
| Status | 28 dp | Icon 16 dp + label 14 sp 600 | No |
| Confidence | 28 dp | Icon + label | No |
| Source | 24 dp | Text only, `surfaceContainer` | No |
| Suggestion | 32 dp visual (48 dp target) | Text | Yes |
| Filter (not MVP) | 32 dp visual (48 dp target) | Text + optional count | Yes |
| Unread dot | 8 dp | — | No |

- Status chip uses the tone mapping in `design-tokens.md`; icon and label always together.
- A chip never truncates the status label; the row wraps instead.
- Interactive chips have a 48 dp invisible target via padding.
- Cluster count is a pill, min 28 dp, `surfaceContainerHigh` + `onSurface`.

## 5. Cards

**Base card**: `surfaceContainer`, 12 dp radius, 16 dp padding, no shadow on light (border
optional). Pressed overlay 12%. Whole card is the target; no nested tappable rows in MVP.

| Card | Anatomy | Status |
|---|---|---|
| Report (map sheet) | Thumbnail 72 + type + time + chip + distance | — |
| Alert | Icon container 40 + title + body line + unread dot + chip | — |
| Verify queue | Thumbnail 72 + type/chip + age + distance + note excerpt | — |
| Evidence | Thumbnail 48 + label + metadata | — |
| Empty/error | Icon 48 + title + body + one action | — |

- Text hierarchy: title 16/600, metadata 14/400 `onSurfaceVariant`, chip 14/600.
- Maximum two lines for body excerpts; full text lives on the detail screen.
- Missing photo → neutral placeholder with **Tanpa foto**; never a broken-image icon.
- Do not show more than one status chip per card.

## 6. Banners

| Banner | Background | Icon | Actions |
|---|---|---|---|
| Offline | `warningContainer` | `cloud_off` | none (informational) |
| Permission needed | `infoContainer` | `notifications_off` / `location_off` | **Aktifkan** / **Buka Pengaturan** |
| Low accuracy | `warningContainer` | `my_location` | none |
| Form error | `errorContainer` | `error_outline` | retry when applicable |
| Stale data | `surfaceContainerHigh` | `schedule` | **Muat ulang** |

- Full width, 12 dp radius, 12–16 dp padding, icon + text; optional single action.
- Dismissible only when the condition does not block the task (offline banner is not blocking).
- Announce appearance to screen readers; do not steal focus from a form.
- Never stack more than two banners; merge or prioritise.

## 7. Bottom sheets

- Top radius 20 dp, drag handle 32×4 dp, scrim 40%.
- Opens at 45% height for marker details, 90% for layers/preferences; content scrolls inside.
- Drag down or tap scrim to close; back closes the sheet before the screen.
- Title 20/600, close icon 48 dp; the primary action stays visible above the safe area.
- A sheet never opens another sheet; replace content or push a page.
- The map stays visible behind the marker sheet; camera does not move on open.
- Focus is trapped inside while open; on close, focus returns to the marker/button.

## 8. Dialogs

- Max width 560 dp (phone: 16 dp margins), 16 dp radius, `surfaceContainerHigh`.
- Title 20/600 + body 16/400 + actions right-aligned (stacked full-width on narrow screens).
- Destructive dialog: title names the action ("Tolak laporan?"), reason field, destructive CTA,
  cancel always present.
- The CTA repeats the action verb; no "OK", no "Ya".
- Dismissing by scrim/back is allowed unless a reason is required mid-submit.
- One dialog at a time; no dialog over a sheet if a sheet action suffices.

## 9. Snackbars

- Bottom, above safe area and navigation; max 4 s; one action.
- Copy is a complete sentence: **Radius peringatan disimpan: 5 km.**
- Never the only confirmation for a destructive action; use a result sheet/dialog.
- Not used for errors that require a decision (use inline error/dialog).

## 10. Empty, loading, error

| State | Anatomy | Rules |
|---|---|---|
| Empty | Icon 48 in `surfaceContainer`, title 20/600, body 14–16, one action | Explain what will appear and how to act; no illustration dependency |
| Loading (content) | Skeleton matching final layout, 1.2 s shimmer | No full-screen spinner for shaped content |
| Loading (action) | Inline button progress + disabled controls | Keep layout stable |
| Error | Icon + DL-0003 message + **Coba lagi** | Cached content stays visible when possible |
| Offline | Banner + cached content | Never replace content with an error page |

## 11. Photo thumbnail

- 72 dp (cards) / 48 dp (evidence) / full width (detail), 8–12 dp radius.
- `BoxFit.cover`; no distortion; 1 dp `outlineVariant` border in dark mode.
- Semantics: "Foto laporan" plus relative time; not the raw file name.
- Placeholder: `surfaceContainerHigh` + `photo_camera` icon + **Tanpa foto** where text fits.
- Never display EXIF or precise location in the UI.

## 12. Map controls

- 48 dp circular buttons on a `surface` background with 1 dp `outline`.
- Stack top-right: layers, locate. Legend bottom-left. Attribution bottom, non-dismissible.
- Buttons sit above the bottom navigation and FAB; never overlap.
- Selected marker: 28 dp + 2 dp focus ring; cluster tap zooms in.
- Every marker has a semantic label ("Laporan warga, 12 menit lalu, terkonfirmasi").

## 13. Accessibility contract (all components)

- Target ≥ 48 dp; spacing between targets ≥ 8 dp.
- Text ≥ 14 sp; supports 200% scale without clipping.
- Contrast from `design-tokens.md`; focus indicators visible in both themes.
- Screen-reader order follows visual order; icon-only controls have labels.
- Status/chip information is available as text, not only as colour/icon.
- Motion respects the OS reduced-motion setting.
- Errors are announced and associated with their field.

## Do / Don't

✅ A verify card uses one status chip, one thumbnail, and a whole-card target.

✅ A disabled safety switch keeps full-contrast label and helper text.

✅ A destructive dialog repeats the verb and requires a reason.

❌ Three stacked banners (offline + permission + low accuracy) pushing the form off-screen.

❌ A bottom sheet with its own bottom sheet for "Tolak" — push a page or use a dialog.

❌ A full-screen spinner for the alert list; use skeleton cards.
