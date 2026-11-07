# Design Tokens — ApiPantau Mobile

| | |
|---|---|
| Task | `AP-008` |
| Owner (values) | QA — Anang |
| Implementation owner | TL / MOB-A — `apps/mobile/lib/core/theme/` |
| Design log | DL-0005 |
| Status | Proposed — supersedes the provisional `AppTokens` on approval |
| Platform | Flutter, Android first; dark mode required |

This is a **specification**, not Dart code. It defines the values and rules; the theme
implementation remains with the seat that owns `apps/mobile/lib/core/`.

## Rules

1. Widgets use semantic tokens only. A hex value or raw `Color(...)` outside
   `core/theme` is a defect.
2. Light and dark are designed together; neither is an afterthought or an automatic inversion.
3. Colour never carries meaning alone. Pair it with an icon and an Indonesian label.
4. Text ≥ 14 sp, tap targets ≥ 48 dp, primary CTA 56 dp. Text scaling to 200% must not clip
   essential content.
5. The platform UI font is used (Roboto on Android; San Francisco on iOS). No font package is
   required. A custom brand font is a TL decision and is out of AP-008.
6. The theme must expose **success, warning, and info** in addition to Material's `error`.
   `ColorScheme.fromSeed` alone cannot express them; how they are exposed is the implementer's
   choice, provided the names and values below are honoured.

## Colour primes

Neutrals are warm so the UI reads as fire/smoke rather than a generic blue-grey product.

| Prime | Hex | Use |
|---|---|---|
| `brand-700` | `#B63A0E` | Light primary |
| `brand-200` | `#FFB59B` | Dark primary |
| `brand-100` | `#FFDCCF` | Light primary container |
| `brand-950` | `#3A0B00` | On light primary container |
| `brand-800` | `#8A2E08` | Dark primary container |
| `neutral-0` | `#FFFFFF` | Cards on light, text on solid |
| `neutral-25` | `#FFFBF8` | Light surface |
| `neutral-50` | `#F6EDE8` | Light surface container |
| `neutral-100` | `#EFE3DD` | Light surface container high |
| `neutral-300` | `#DCC5BB` | Light outline variant (decorative) |
| `neutral-500` | `#8C7166` | Light outline (essential borders) |
| `neutral-700` | `#5C4A42` | Light secondary text |
| `neutral-900` | `#1F1B18` | Light primary text |
| `neutral-950` | `#171210` | Dark surface |
| `neutral-800` | `#251D19` | Dark surface container |
| `neutral-750` | `#332823` | Dark surface container high |
| `neutral-400` | `#CBB4A9` | Dark secondary text |
| `neutral-550` | `#A88B7F` | Dark outline |
| `neutral-650` | `#5A4A42` | Dark outline variant (decorative) |

## Semantic colour roles

| Token | Light | Dark | Usage |
|---|---|---|---|
| `color.surface` | `#FFFBF8` | `#171210` | Screen background |
| `color.surfaceContainer` | `#F6EDE8` | `#251D19` | Cards, list rows, neutral chips |
| `color.surfaceContainerHigh` | `#EFE3DD` | `#332823` | Sheets, raised cards, pressed states |
| `color.onSurface` | `#1F1B18` | `#EFE1DA` | Primary text, icons |
| `color.onSurfaceVariant` | `#5C4A42` | `#CBB4A9` | Secondary text, metadata |
| `color.outline` | `#8C7166` | `#A88B7F` | Input borders, essential dividers |
| `color.outlineVariant` | `#DCC5BB` | `#5A4A42` | Decorative dividers only |
| `color.primary` | `#B63A0E` | `#FFB59B` | Primary CTA, links, focus |
| `color.onPrimary` | `#FFFFFF` | `#5C1A00` | Text/icon on primary |
| `color.primaryContainer` | `#FFDCCF` | `#8A2E08` | Brand-tinted surfaces |
| `color.onPrimaryContainer` | `#3A0B00` | `#FFDCCF` | Content on brand container |
| `color.success` | `#1B6B3A` | `#8FDFA8` | Confirmed text/icon |
| `color.onSuccess` | `#FFFFFF` | `#00391A` | Content on solid success |
| `color.successContainer` | `#C8F2D6` | `#0B5228` | Confirmed chips/cards |
| `color.onSuccessContainer` | `#0B3D1F` | `#C8F2D6` | Content on confirmed chip |
| `color.successStrong` | `#145C32` | `#1E6B3A` | `terkonfirmasi_ganda` solid chip |
| `color.onSuccessStrong` | `#FFFFFF` | `#FFFFFF` | Content on strong success |
| `color.warning` | `#7A4B00` | `#FFD180` | Watching/accuracy warnings |
| `color.onWarning` | `#FFFFFF` | `#3F2A00` | Content on solid warning |
| `color.warningContainer` | `#FFE2A8` | `#5B3E00` | Warning banners/chips |
| `color.onWarningContainer` | `#261700` | `#FFE2A8` | Content on warning container |
| `color.error` | `#B3261E` | `#FFB4AB` | Active incident, blocking errors |
| `color.onError` | `#FFFFFF` | `#690005` | Content on solid error |
| `color.errorContainer` | `#F9DEDC` | `#93000A` | Rejected chips, destructive dialogs |
| `color.onErrorContainer` | `#410E0B` | `#FFDAD6` | Content on error container |
| `color.info` | `#1A5CA8` | `#AECBFF` | Handled, links, neutral-positive |
| `color.onInfo` | `#FFFFFF` | `#002F60` | Content on solid info |
| `color.infoContainer` | `#D8E6FF` | `#15457D` | Info chips/banners |
| `color.onInfoContainer` | `#001B3B` | `#D8E6FF` | Content on info container |
| `color.scrim` | `#000000` 40% | `#000000` 40% | Modal/sheet scrim |
| `color.disabled` | `onSurface` 38% | `onSurface` 38% | Disabled content (never sole carrier of required info) |

### Status tone mapping

Use these exact pairings; do not invent a sixth tone.

| Tone | Background | Content | Used by |
|---|---|---|---|
| neutral | `surfaceContainer` | `onSurfaceVariant` | `menunggu_verifikasi`, `selesai`, cluster count |
| success | `successContainer` | `onSuccessContainer` | `terkonfirmasi` |
| successStrong | `successStrong` | `onSuccessStrong` | `terkonfirmasi_ganda` |
| warning | `warningContainer` | `onWarningContainer` | `terpantau`, low-accuracy warning |
| error | `errorContainer` | `onErrorContainer` | `ditolak`, destructive dialog |
| info | `infoContainer` | `onInfoContainer` | `ditangani`, `terkendali`, offline/neutral notices |

Incident **map markers** are solid semantic colours with their `on*` pair and a 2 dp surface
halo: error for `aktif`, warning for `terpantau`, info for `terkendali`, neutral for `selesai`.

## Contrast verification (WCAG 2.1)

Measured with the standard relative-luminance formula. Text pairs target ≥ 4.5:1; essential
icons/borders target ≥ 3:1. Decorative dividers (`outlineVariant`) are exempt.

| Pair | Ratio | Requirement | Result |
|---|---|---|---|
| Light `onSurface` / `surface` | 16.61 | 4.5 | Pass |
| Light `onSurfaceVariant` / `surface` | 8.12 | 4.5 | Pass |
| Light `onSurfaceVariant` / `surfaceContainer` | 7.24 | 4.5 | Pass |
| Light `onSurfaceVariant` / `surfaceContainerHigh` | 6.65 | 4.5 | Pass |
| Light `primary` / `surface` | 5.67 | 4.5 | Pass |
| Light `onPrimary` / `primary` | 5.83 | 4.5 | Pass |
| Light `onPrimaryContainer` / `primaryContainer` | 13.35 | 4.5 | Pass |
| Light `error` / `surface` | 6.35 | 4.5 | Pass |
| Light `onError` / `error` | 6.54 | 4.5 | Pass |
| Light `onErrorContainer` / `errorContainer` | 12.77 | 4.5 | Pass |
| Light `success` / `surface` | 6.36 | 4.5 | Pass |
| Light `onSuccess` / `success` | 6.54 | 4.5 | Pass |
| Light `onSuccessContainer` / `successContainer` | 10.07 | 4.5 | Pass |
| Light `onSuccessStrong` / `successStrong` | 8.06 | 4.5 | Pass |
| Light `warning` / `surface` | 7.20 | 4.5 | Pass |
| Light `onWarning` / `warning` | 7.41 | 4.5 | Pass |
| Light `onWarningContainer` / `warningContainer` | 13.86 | 4.5 | Pass |
| Light `info` / `surface` | 6.50 | 4.5 | Pass |
| Light `onInfo` / `info` | 6.69 | 4.5 | Pass |
| Light `onInfoContainer` / `infoContainer` | 13.68 | 4.5 | Pass |
| Light `outline` / `surface` | 4.37 | 3.0 | Pass |
| Dark `onSurface` / `surface` | 14.55 | 4.5 | Pass |
| Dark `onSurfaceVariant` / `surface` | 9.41 | 4.5 | Pass |
| Dark `onSurfaceVariant` / `surfaceContainer` | 8.39 | 4.5 | Pass |
| Dark `onSurfaceVariant` / `surfaceContainerHigh` | 7.25 | 4.5 | Pass |
| Dark `primary` / `surface` | 10.91 | 4.5 | Pass |
| Dark `onPrimary` / `primary` | 7.70 | 4.5 | Pass |
| Dark `onPrimaryContainer` / `primaryContainer` | 6.62 | 4.5 | Pass |
| Dark `error` / `surface` | 10.94 | 4.5 | Pass |
| Dark `onError` / `error` | 7.72 | 4.5 | Pass |
| Dark `onErrorContainer` / `errorContainer` | 7.24 | 4.5 | Pass |
| Dark `success` / `surface` | 11.76 | 4.5 | Pass |
| Dark `onSuccess` / `success` | 8.30 | 4.5 | Pass |
| Dark `onSuccessContainer` / `successContainer` | 7.61 | 4.5 | Pass |
| Dark `onSuccessStrong` / `successStrong` | 6.52 | 4.5 | Pass |
| Dark `warning` / `surface` | 12.99 | 4.5 | Pass |
| Dark `onWarning` / `warning` | 9.52 | 4.5 | Pass |
| Dark `onWarningContainer` / `warningContainer` | 7.82 | 4.5 | Pass |
| Dark `info` / `surface` | 11.31 | 4.5 | Pass |
| Dark `onInfo` / `info` | 8.12 | 4.5 | Pass |
| Dark `onInfoContainer` / `infoContainer` | 7.66 | 4.5 | Pass |
| Dark `outline` / `surface` | 5.90 | 3.0 | Pass |
| Map hotspot glyph / hotspot | 6.47 | 4.5 | Pass |
| Map report glyph / report | 6.69 | 4.5 | Pass |
| Map warning glyph / typical light tile | 6.48 | 4.5 | Pass |
| Map error glyph / typical light tile | 5.72 | 4.5 | Pass |

The current provisional primary `#D84315` is **not** used: white on it is below 4.5:1. This is
the reason for the value change in DL-0005 Q13.

## Map encoding

| Element | Fill | Glyph | Shape | Note |
|---|---|---|---|---|
| Satellite hotspot | `#F59E0B` | `#3A2A00` | Diamond, 12–16 dp | Dark 1 dp outline; low visual weight |
| Citizen report | `#1A5CA8` | `#FFFFFF` | Circle, 20 dp | Camera glyph; cluster number replaces glyph |
| Incident `aktif` | `color.error` | `color.onError` | Ring 2 dp + 20 dp dot | Area fill 16% |
| Incident `terpantau` | `color.warning` | `color.onWarning` | Ring 2 dp + 20 dp dot | Area fill 16% |
| Incident `terkendali` | `color.info` | `color.onInfo` | Ring 2 dp + 20 dp dot | Area fill 16% |
| Incident `selesai` | `onSurfaceVariant` | `surface` | Ring 2 dp + 16 dp dot | Area fill 10% |
| User location | `color.info` | — | 16 dp dot + 24% halo | Halo never intercepts taps |
| Cluster | `surfaceContainerHigh` | `onSurface` | Pill, min 28 dp | Count text 14 sp semibold |

Rules: every marker has a 2 dp `surface` halo; selection adds a 2 dp focus ring; markers never
change size on hover (no hover on touch); the legend repeats shape + icon + label.

## Typography

| Token | Size / line | Weight | Usage |
|---|---|---|---|
| `type.headline` | 24 / 34 | 700 | Screen titles, result-sheet title |
| `type.title` | 20 / 28 | 600 | Section titles, incident title |
| `type.subtitle` | 16 / 24 | 600 | Card titles, list lead |
| `type.body` | 16 / 24 | 400 | Notes, paragraphs, form text |
| `type.bodySmall` | 14 / 20 | 400 | Metadata, secondary lines |
| `type.label` | 14 / 20 | 600 | Buttons, chips, tabs, field labels |
| `type.caption` | 14 / 20 | 500 | Timestamps, counters, helper text |
| `type.metric` | 28 / 38 | 700 | Distance/count emphasis, tabular figures |

- Minimum is **14 sp** everywhere, including captions and helper text. Do not introduce 12 sp.
- Line height ≥ 1.35; body 1.5.
- No all-caps strings; they harm readability and localisation.
- Number formatting: Indonesian thousands `.`, decimal `,`; time 24 h (`14.05`); date
  `7 Nov 2026`; relative time below 24 h.
- Support system text scale up to 200%: no fixed-height text containers; buttons and rows grow;
  critical labels wrap rather than ellipsize.

## Spacing

| Token | dp | Typical use |
|---|---|---|
| `space.1` | 4 | Icon-to-text tight, badge offset |
| `space.2` | 8 | Inline gap, chip gap |
| `space.3` | 12 | List item gap, card inner gap |
| `space.4` | 16 | Screen margin, card padding, bottom bar inset |
| `space.5` | 20 | Sheet padding |
| `space.6` | 24 | Section gap, sheet top gap |
| `space.8` | 32 | Empty-state gap, large block separation |
| `space.10` | 40 | Hero/empty illustration spacing |
| `space.12` | 48 | Minimum target, large vertical rhythm |
| `space.16` | 64 | Splash/empty top offset |

Layout: 4 dp baseline grid; screen margin 16; content max width 560 on tablets; phone-first.
Bottom action bars use 16 dp inset plus the system safe area. The map FAB sits 16 dp from the
edges and above the bottom navigation, never over attribution.

## Sizes, radius, elevation

| Token | Value | Use |
|---|---|---|
| `size.tap` | 48 dp | Every interactive target, minimum |
| `size.cta` | 56 dp | Primary filled button height |
| `size.input` | 56 dp | Text field height |
| `size.icon` | 24 dp | Standard icon |
| `size.iconSmall` | 20 dp | Inline metadata icon |
| `size.thumb` | 72 dp | Report thumbnail |
| `size.avatar` | 40 dp | Reporter/verifier avatar |
| `size.fab` | 56 dp | Lapor FAB |
| `size.bottomNav` | 80 dp | Bottom navigation + safe area |
| `radius.sm` | 8 dp | Chips, thumbnails |
| `radius.md` | 12 dp | Cards, buttons, inputs |
| `radius.lg` | 16 dp | Photo preview, large cards |
| `radius.sheet` | 20 dp top | Bottom sheets |
| `radius.full` | 999 dp | Pills, unread dot |
| `elevation.0` | none | Flat surfaces, list rows |
| `elevation.1` | 2 dp | Cards, FAB |
| `elevation.2` | 4 dp | Sheets, sticky bars |
| `elevation.3` | 8 dp | Dialogs (max) |

Prefer a 1 dp `outlineVariant` border over a shadow on light surfaces. In dark mode, express
elevation with `surfaceContainer` / `surfaceContainerHigh`, not larger shadows.

## Motion

| Token | Value | Use |
|---|---|---|
| `motion.micro` | 120 ms | Press, chip select, icon swap |
| `motion.enter` | 200 ms | List item, banner, page content |
| `motion.sheet` | 300 ms | Bottom sheet open/close |
| `easing.standard` | cubic-bezier(0.2, 0, 0, 1) | Default |
| `easing.exit` | cubic-bezier(0.4, 0, 1, 1) | Dismissal |

- Respect the OS "remove animations" setting: replace motion with an instant state change.
- No looping animation except an indeterminate progress indicator; no parallax.
- Loading skeletons use a subtle 1.2 s shimmer or a static placeholder; never a flashing block.

## Opacity

| Token | Value | Use |
|---|---|---|
| `opacity.disabled` | 38% | Disabled text/icon |
| `opacity.pressed` | 12% | Pressed overlay |
| `opacity.halo` | 24% | Location accuracy halo |
| `opacity.areaFill` | 16% | Incident area fill (`10%` for `selesai`) |
| `opacity.scrim` | 40% | Modal/sheet scrim |

## Implementation contract

- Replace the provisional constants in `apps/mobile/lib/core/theme/app_tokens.dart:5` with the
  semantic set above. `seed`, `minTapTarget`, and `minBodyText` remain valid constraints but the
  final theme is not a single-seed derivation.
- Keep the current minimum-text enforcement in `apps/mobile/lib/core/theme/app_theme.dart:20`
  and extend it to every text role.
- Keep the existing Indonesian failure strings
  (`apps/mobile/lib/core/l10n/app_strings.dart:40`); the token work must not rename copy.
- No new dependency, font, or asset is required by this specification.
- The implementation must pass a widget check for: 48 dp targets on every button/icon, 14 sp
  minimum, light/dark contrast, and 200% text scale without overflow.

## Do / Don't

✅ A status chip uses `successContainer` + `onSuccessContainer` + check icon + "Terkonfirmasi".

✅ A disabled safety switch is visibly disabled but its label and helper text remain at full
contrast.

✅ Sheet elevation uses `surfaceContainerHigh`; the scrim is 40% black.

❌ `Text('Terkonfirmasi', style: TextStyle(color: Colors.green))` — no token, no icon, fails
contrast in one theme.

❌ Pure black `#000000` surface in dark mode; it creates halation on OLED and loses the warm
product tone.

❌ A 12 sp caption "12 menit lalu" because it "fits better"; the minimum is 14 sp.

## Verification checklist

- [ ] Every semantic token has a light and dark value; no token is light-only.
- [ ] Ratios in the table are reproducible; no pair used by text is below 4.5:1.
- [ ] Widgets contain no hex/`Color(...)` values outside `core/theme`.
- [ ] All targets are ≥ 48 dp; primary CTA is 56 dp.
- [ ] All text roles are ≥ 14 sp; 200% scale does not clip critical content.
- [ ] Status chips use the tone mapping and include an icon + label.
- [ ] Map markers remain distinguishable in both themes and on satellite imagery.
- [ ] Reduced-motion and dark-mode checks pass on a physical Android device.
