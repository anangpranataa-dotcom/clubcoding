# Copy Deck — Bahasa Indonesia

| | |
|---|---|
| Task | `AP-008` |
| Owner | QA — Anang |
| Consumers | MOB-A, MOB-B, BE (push payloads), WEB (status vocabulary) |
| Design log | DL-0005 |
| Status | Proposed |

Single source of truth for user-facing Indonesian copy. If a string is missing, add an ID here
before implementing it. Do not paraphrase in widgets, and do not ship English SDK text.

## Voice and rules

1. **Calm, direct, respectful.** Address the user as **Anda**, never "kamu" or "user".
2. **No blame.** "Laporan belum bisa dikirim" — not "Anda gagal mengirim".
3. **No technical jargon.** Say "luring"/"daring" (the PRD terms), "jejaring", "radius"; never
   SQL status, HTTP code, UUID, "sinkronisasi", "payload", or an exception message.
4. **Sentence case.** Titles and buttons use sentence case; the brand is **ApiPantau**.
5. **No exclamation marks, no emoji.** Urgency comes from the icon, tone, and wording.
6. **Buttons name the action.** "Tolak laporan", not "OK"; "Buang", not "Ya".
7. **One meaning per word.** "Laporan" = citizen report; "kejadian" = incident; "titik panas" =
   satellite hotspot; "peringatan" = alert/notification.
8. **Numbers and time follow Indonesian convention:** `1.000`, `3,2 km`, `14.05`, `7 Nov 2026`.
9. **Relative time** below 24 h; absolute time otherwise. "Baru saja" under 1 minute.
10. **Distance** uses `±` and one decimal for km: `±3,2 km`; below 1 km use metres: `±450 m`.
    Unknown location hides distance rather than guessing.

## Navigation and global

| ID | Context | Copy |
|---|---|---|
| `C-001` | App name | ApiPantau |
| `C-002` | Bottom nav — map | Peta |
| `C-003` | Bottom nav — alerts | Peringatan |
| `C-004` | Bottom nav — verify | Verifikasi |
| `C-005` | Bottom nav — profile | Profil |
| `C-006` | Primary report action | Lapor |
| `C-007` | Generic retry | Coba lagi |
| `C-008` | Back to map | Kembali ke peta |
| `C-009` | Settings link | Buka Pengaturan |
| `C-010` | Close | Tutup |
| `C-011` | Cancel | Batal |
| `C-012` | Save confirmation pattern | Tersimpan. |
| `C-013` | Offline banner title | Anda sedang luring |
| `C-014` | Offline report helper | Laporan tetap bisa dibuat dan akan dikirim otomatis. |

## Report flow (`01-report.md`)

| ID | Context | Copy |
|---|---|---|
| `C-100` | FAB label | Lapor |
| `C-101a` | Location rationale title | Izinkan lokasi? |
| `C-101b` | Location rationale body | Lokasi dipakai untuk menandai titik asap/api dan mengirim peringatan di sekitar Anda. Titik laporan terlihat publik; lokasi rumah Anda tidak ditampilkan. |
| `C-101c` | Location rationale primary | Izinkan lokasi |
| `C-101d` | Location rationale secondary | Pilih lokasi manual |
| `C-102a` | Camera rationale title | Izinkan kamera? |
| `C-102b` | Camera rationale body | Kamera dipakai untuk memotret asap atau api. Foto dikompres sebelum diunggah dan data lokasi foto (EXIF) dihapus. |
| `C-102c` | Camera rationale primary | Izinkan kamera |
| `C-102d` | Camera rationale secondary | Pilih dari galeri |
| `C-103` | Review app bar | Tinjau laporan |
| `C-104` | Replace photo | Ganti foto |
| `C-105` | Remove photo | Hapus |
| `C-106` | Map caption | Titik laporan |
| `C-107` | Recenter to GPS | Lokasi saya |
| `C-108` | Low accuracy warning | Akurasi lokasi rendah (±{akurasi} m). Geser pin bila perlu. |
| `C-109` | No GPS | Lokasi belum tersedia. Geser pin ke titik asap/api. |
| `C-110` | Note label | Catatan (opsional) |
| `C-111` | Suggestion chip | Asap tebal |
| `C-112` | Suggestion chip | Sudah ada api |
| `C-113` | Suggestion chip | Bau terbakar |
| `C-114` | Privacy note | Lokasi laporan akan terlihat publik; lokasi rumah Anda tidak. |
| `C-115` | Submit | Kirim laporan |
| `C-116` | Compression state | Menyiapkan foto… |
| `C-117` | Upload state | Mengirim… |
| `C-118a` | Discard dialog title | Buang laporan? |
| `C-118b` | Discard dialog body | Foto dan catatan yang sudah diisi akan hilang. |
| `C-118c` | Discard dialog keep | Lanjut mengisi |
| `C-118d` | Discard dialog discard | Buang |
| `C-119a` | Success title | Laporan terkirim |
| `C-119b` | Success body | Verifikator akan memeriksa laporan Anda. |
| `C-120a` | Offline result title | Laporan tersimpan |
| `C-120b` | Offline chip | Terkirim (luring) |
| `C-120c` | Offline body | Laporan akan dikirim otomatis saat sinyal kembali. |
| `C-121` | Photo required | Laporan membutuhkan satu foto. |
| `C-122` | Location required | Tentukan lokasi laporan. |
| `C-123` | Success secondary action | Lihat laporan saya |
| `C-124` | Success primary action | Kembali ke peta |
| `C-125` | Rate limit | Terlalu banyak laporan. Coba lagi dalam {menit} menit. |
| `C-126` | Photo upload failure | Foto gagal diunggah. Coba lagi. |
| `C-127` | Offline entry banner body | Laporan tetap bisa dibuat dan akan dikirim otomatis. |
| `C-129` | Note field hint | Tambahkan catatan bila ada detail penting (opsional). |

## Map and incident (`02-map-incident.md`)

| ID | Context | Copy |
|---|---|---|
| `C-200` | Map app bar | Peta |
| `C-201` | Map subtitle | Kejadian di sekitar Anda |
| `C-202` | Layer sheet title | Layer peta |
| `C-203` | Layer | Kejadian |
| `C-204` | Layer | Titik panas satelit |
| `C-205` | Layer | Laporan warga |
| `C-206` | Legend control | Legenda |
| `C-207` | Empty viewport | Tidak ada kejadian di area ini. |
| `C-208` | Empty action | Perluas peta |
| `C-209` | Map loading | Memuat peta… |
| `C-210` | Offline map | Peta luring — data mungkin belum terbaru. |
| `C-211` | Location banner | Aktifkan lokasi untuk melihat kejadian di sekitar Anda. |
| `C-212` | Location action | Aktifkan lokasi |
| `C-213` | Sheet type — report | Laporan warga |
| `C-214` | Sheet type — hotspot | Titik panas satelit |
| `C-215` | Sheet type — incident | Kejadian |
| `C-216` | Relative time pattern | {waktu} lalu |
| `C-217a` | Distance km | ±{jarak} km dari lokasi Anda |
| `C-217b` | Distance m | ±{jarak} m dari lokasi Anda |
| `C-218` | Open detail | Lihat detail |
| `C-219` | Incident detail title | Kejadian |
| `C-220` | Radius section | Radius peringatan |
| `C-221` | Radius helper | Peringatan dikirim saat kejadian terkonfirmasi di dalam radius ini. |
| `C-222` | Radius saved | Radius peringatan disimpan: {km} km. |
| `C-223` | Ended incident | Kejadian ini sudah selesai. |
| `C-224` | Show on map | Lihat di peta |
| `C-225` | Coordinates disclosure | Lihat koordinat |
| `C-226` | Hotspot empty | Tidak ada titik panas dalam 7 hari. |
| `C-227` | Report empty | Belum ada laporan warga. |
| `C-228` | Evidence count | {laporan} laporan, {titik} titik panas |
| `C-229` | Incident not found | Kejadian tidak ditemukan |
| `C-230` | GPS unavailable chip | Lokasi belum tersedia |
| `C-231` | Satellite attribution | Esri World Imagery |
| `C-232` | OSM attribution | © OpenStreetMap contributors |
| `C-233` | Layer updated label | Terakhir diperbarui {waktu} |
| `C-234` | Sheet loading | Memuat detail… |

## Alerts and push (`03-alerts.md`)

| ID | Context | Copy |
|---|---|---|
| `C-300` | Alerts app bar | Peringatan |
| `C-301a` | Notification rationale title | Aktifkan peringatan |
| `C-301b` | Notification rationale body | Peringatan dikirim saat ada kejadian terkonfirmasi di radius {km} km dari Anda. Titik panas satelit mentah tidak dikirim ke warga. |
| `C-301c` | Notification rationale primary | Aktifkan notifikasi |
| `C-301d` | Notification rationale secondary | Nanti saja |
| `C-302` | Preferences action | Preferensi |
| `C-303` | Notification off helper | Notifikasi dimatikan. Anda tetap bisa melihat peringatan di tab ini. |
| `C-304` | Mandatory safety helper | Peringatan keselamatan untuk kejadian aktif dalam 2 km selalu aktif. |
| `C-305` | Permission not asked banner | Aktifkan peringatan agar tidak melewatkan kejadian di sekitar Anda. |
| `C-306` | Permission denied banner | Notifikasi dimatikan di pengaturan perangkat. |
| `C-307a` | Alerts empty title | Belum ada peringatan |
| `C-307b` | Alerts empty body | Peringatan muncul saat ada kejadian terkonfirmasi di radius Anda. |
| `C-307c` | Alerts empty action | Atur radius |
| `C-308` | Alerts offline | Anda sedang luring. Daftar mungkin belum terbaru. |
| `C-309` | Push title — fire | Peringatan: api terkonfirmasi ±{jarak} km |
| `C-310` | Push body — fire | Asap tebal di {wilayah}. {waktu} lalu. Sumber: {sumber}. |
| `C-311` | Push title — escalation | Peringatan diperbarui: api semakin luas |
| `C-312` | Push body — escalation | Kejadian di {wilayah} meningkat. {waktu} lalu. Sumber: {sumber}. |
| `C-313` | Foreground banner action | Lihat |
| `C-314` | Push title — smoke | Peringatan: asap terkonfirmasi ±{jarak} km |
| `C-315` | Push body — smoke | Asap tebal terlihat di {wilayah}. {waktu} lalu. Sumber: {sumber}. |
| `C-316` | List heading | Hari ini |
| `C-317` | List heading | Kemarin |
| `C-318` | Reload | Muat ulang |
| `C-319` | Missing incident | Kejadian tidak ditemukan |
| `C-320` | Preferences title | Preferensi peringatan |
| `C-321` | Notification status on | Notifikasi: Aktif |
| `C-322` | Notification status off | Notifikasi: Dimatikan |
| `C-323` | Radius label | Radius |
| `C-324` | Type — new incident | Kejadian baru di radius |
| `C-325` | Type — escalation | Eskalasi kejadian |
| `C-326` | Type — new report (verifier) | Laporan baru di sekitar |
| `C-327` | Type — new hotspot (verifier) | Titik panas satelit baru |
| `C-328` | Type — mandatory safety | Peringatan keselamatan < 2 km |
| `C-329` | Preferences save failed | Preferensi gagal disimpan. Coba lagi. |
| `C-330` | Radius saved snackbar | Radius peringatan disimpan: {km} km. |

## Verification (`04-verify.md`)

| ID | Context | Copy |
|---|---|---|
| `C-400` | Verify app bar | Verifikasi |
| `C-401` | Queue count | Verifikasi ({jumlah}) |
| `C-402` | Sort explanation | Diurutkan: jarak ke kejadian aktif, lalu waktu. |
| `C-403` | Waiting age | Menunggu {menit} menit |
| `C-404` | Distance to incident | ±{jarak} dari kejadian aktif |
| `C-405` | No linked incident | Tidak terkait kejadian aktif |
| `C-406` | Missing photo | Tanpa foto |
| `C-407a` | Queue empty title | Antrean bersih |
| `C-407b` | Queue empty body | Tidak ada laporan yang menunggu verifikasi. |
| `C-407c` | Queue empty action | Muat ulang |
| `C-408` | New items pill | {jumlah} laporan baru |
| `C-409` | Detail app bar | Verifikasi laporan |
| `C-410` | No note | Tidak ada catatan. |
| `C-411a` | Action | Konfirmasi |
| `C-411b` | Action | Butuh info |
| `C-411c` | Action | Tolak |
| `C-412` | Reason too short | Alasan minimal 10 karakter. |
| `C-413a` | Confirm dialog title | Konfirmasi laporan? |
| `C-413b` | Confirm dialog body | Laporan akan berstatus terkonfirmasi dan dapat memicu peringatan radius. |
| `C-413c` | Confirm note label | Catatan (opsional) |
| `C-413d` | Confirm CTA | Konfirmasi laporan |
| `C-414a` | Info request title | Minta informasi tambahan |
| `C-414b` | Info request field | Apa yang perlu dilengkapi? |
| `C-414c` | Info request CTA | Kirim permintaan |
| `C-415a` | Reject dialog title | Tolak laporan? |
| `C-415b` | Reject field | Alasan penolakan |
| `C-415c` | Reject CTA | Tolak laporan |
| `C-416a` | Confirm success | Laporan terkonfirmasi |
| `C-416b` | Confirm success action | Laporan berikutnya |
| `C-417a` | Double confirm result | Terkonfirmasi ganda |
| `C-417b` | Double confirm body | Peringatan radius dikirim. |
| `C-418a` | Info request success | Permintaan terkirim |
| `C-418b` | Info request success body | Pelapor akan melihat permintaan ini. |
| `C-419a` | Reject success | Laporan ditolak |
| `C-419b` | Reject success body | Alasan tercatat di audit. |
| `C-420a` | Reporter-facing request title | Verifikator meminta informasi tambahan |
| `C-420b` | Reporter-facing request body | {catatan} |
| `C-420c` | Reporter-facing action | Tambah informasi |
| `C-421a` | Conflict title | Laporan ini sudah diproses |
| `C-421b` | Conflict body | Status saat ini: {status}. |
| `C-421c` | Conflict action | Muat ulang antrean |
| `C-422` | Verify offline | Verifikasi membutuhkan koneksi. |
| `C-423` | Empty audit | Belum ada tindakan. |
| `C-424` | Audit disclosure | Lihat riwayat |
| `C-425` | Report missing | Laporan tidak ditemukan. |
| `C-426` | Photo unavailable | Foto tidak tersedia |
| `C-427a` | Audit — confirmed | Dikonfirmasi oleh {nama} |
| `C-427b` | Audit — rejected | Ditolak oleh {nama} |
| `C-427c` | Audit — info | Diminta info oleh {nama} |
| `C-428` | Next report | Laporan berikutnya |
| `C-429` | Back to queue | Kembali ke antrean |
| `C-430` | Role denied | Anda tidak punya akses. |

## Status vocabulary

Use this mapping everywhere: map, list, sheet, audit, notification.

| ID | Database value | Label | Tone | Icon |
|---|---|---|---|---|
| `C-500` | `menunggu_verifikasi` | Menunggu verifikasi | neutral | `schedule` |
| `C-501` | `terkonfirmasi` | Terkonfirmasi | success | `check_circle` |
| `C-502` | `terkonfirmasi_ganda` | Terkonfirmasi ganda | successStrong | `verified` |
| `C-503` | `ditolak` | Ditolak | error | `cancel` |
| `C-504` | `ditangani` | Ditangani | info | `task_alt` |
| `C-510` | `terpantau` | Terpantau | warning | `visibility` |
| `C-511` | `aktif` | Aktif | error | `local_fire_department` |
| `C-512` | `terkendali` | Terkendali | info | `shield` |
| `C-513` | `selesai` | Selesai | neutral | `check_circle` |

**Confidence**

| ID | Value | Label |
|---|---|---|
| `C-520` | `rendah` / `low` | Keyakinan rendah |
| `C-521` | `sedang` / `nominal` | Keyakinan sedang |
| `C-522` | `tinggi` / `high` | Keyakinan tinggi |
| `C-523` | missing/unknown | Keyakinan belum tersedia |

**Source**

| ID | Value | Label |
|---|---|---|
| `C-530` | report | Warga |
| `C-531` | satellite | Satelit |
| `C-532` | both | Warga + satelit |

## Shared failure copy (owned by DL-0003)

Do **not** redefine these in a feature. Use the existing constants in
`apps/mobile/lib/core/l10n/app_strings.dart:40`.

| Constant | Copy |
|---|---|
| `failureNetwork` | Tidak ada koneksi. Coba lagi. |
| `failureAuth` | Sesi atau kode tidak valid. |
| `failurePermission` | Anda tidak punya akses. |
| `failureValidation` | Data tidak valid. |
| `failureServer` | Server sedang bermasalah. |
| `failureUnknown` | Terjadi kesalahan. |

Feature-specific additions (rate limit, photo upload, conflict) are above and must map from a
distinguishable server response; if the backend cannot distinguish them, use the generic
`failureUnknown` rather than guessing.

## String checks

- [ ] Every string in a flow doc has an ID here.
- [ ] No raw database value or English SDK text is rendered.
- [ ] Placeholders use `{...}` and are documented by context.
- [ ] "Anda" is used consistently; no "kamu".
- [ ] No exclamation marks or emoji.
- [ ] Buttons name the action, not "OK"/"Ya".
- [ ] Relative time, distance, and number formats follow the rules above.
