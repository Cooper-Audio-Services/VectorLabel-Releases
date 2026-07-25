# Changelog

All notable changes to VectorLabel are recorded here. **This file is the single source
of truth for what changed between versions** — every fix and feature lands under
`[Unreleased]` as it's made, and moves under a dated version heading when that version
is released. The website's [Downloads page](https://vectorlabel.cooperaudioservices.com/downloads.html)
is built from these entries so users can see the changes between each release.

The format follows [Keep a Changelog](https://keepachangelog.com/); versions are
`MAJOR.MINOR.PATCH` (in [`/VERSION`](VERSION)). Each build also carries a monotonic build
number (git commit count) + short SHA, shown in the menu-bar footer.

## [Unreleased]

## [1.16.0] — 2026-07-25

### Added
- **Send-feedback form on the website** — a new page to report a bug or request a feature
  without a GitHub account. It goes straight to the developer; a quick anti-spam check keeps
  out bots.

### Changed
- **In-app problem reports now go to the developer's private repository through the website.**
  The "Report a Problem" flow is unchanged for you — this just consolidates where reports land
  (the separate reports repository is being retired). Older installs keep working until updated.

## [1.15.5] — 2026-07-23

### Fixed
- **Installing an update really only opens one installer now.** The previous fix (1.15.3)
  still left a gap: the safeguard was set only after the installer was handed off, so a
  second trigger (the update prompt and the Preferences ▸ Updates card both offer "Update
  Now") could still slip a second installer through. The app now commits to the update the
  instant you start it, so no duplicate can begin.

## [1.15.4] — 2026-07-23

### Fixed
- **The Designer's "Margins" button now turns the label's blue boundary line on and off.**
  Previously the blue printable-area outline was always shown and the Margins button only
  toggled the printer's unprintable-margin shading — which is invisible when no printer is
  selected, so the button looked like it did nothing. The button now controls the blue
  outline too (the white label stays visible either way).

## [1.15.3] — 2026-07-23

### Added
- **"Borders" toggle in the Designer toolbar.** Turn it on to outline every text box on the
  canvas so you can see its exact bounds while designing. It's a design aid only — the
  outline never appears in the Print window preview or on the printed label. The setting is
  remembered between sessions.

### Changed
- **Auto-sync designs prompt to relocate a missing data file when opened.** If you reopen a
  Custom Designer design that has auto-sync turned on and its linked CSV/Excel file can't be
  found, it now asks you to locate the file right away (auto-sync needs the live file). The
  label still opens with its saved copy of the data if you cancel. Designs without auto-sync
  are unchanged — they only ask when you choose "Refresh from source".

### Fixed
- **Installing an update no longer opens two installers.** The updater could hand the
  downloaded installer off twice (there's an "Update Now" in both the update prompt and
  Preferences ▸ Updates, and the download guard reopened as soon as the download finished).
  The hand-off is now strictly one-shot.

## [1.15.2] — 2026-07-22

### Added
- **Remove a bound database in the Custom Designer.** Click the data-file name in the
  Database pane and choose **Remove database…** to unbind the data and return the design
  to a single (non-data) label. It confirms first, and warns if objects on the label pull
  from the data (they keep their bindings and simply show blank until a database with those
  columns is added again).

### Fixed
- **Static text honors the line breaks you type.** With **Wrap text** OFF, pressing Enter
  inside a text box now starts a new line on the label exactly as typed (it used to collapse
  onto one line). With **Wrap text** ON, the app keeps deciding line breaks by width and
  ignores your manual returns, as before. The on-screen preview and the printed label now
  match in both modes.

## [1.15.1] — 2026-07-20

### Changed
- **First-launch setup defaults starter templates to install on a fresh install, but to
  skip on an update.** A new user gets the starter templates offered ready to install; an
  existing user updating the app no longer has them re-offered by default (they'd already
  have them) — each template can still be turned on per row, or all at once with the
  preset button. Opening the window manually from Preferences also defaults to skip.
- **"Install all & clear existing" now covers starter templates too.** The setup
  window's preset button previously only reset the supply groups; it now also flips
  every starter template to Install & Replace, so one click yields a clean factory
  set of both supplies and templates (a same-named template is overwritten, never
  duplicated).

## [1.15.0] — 2026-07-20

### Added
- **The Engine now keeps Auto Print running.** If Auto Print isn't running — it crashed,
  was quit, or never started — the Engine relaunches it within about 20 seconds, so
  Vectorworks exports can't silently go unnoticed while nothing is watching the export
  folder. This also means "Launch at login" on the Engine now effectively covers
  Auto Print too. (If Auto Print keeps dying instantly, the Engine stops retrying after
  3 attempts in 5 minutes and notes it in the log instead of retrying forever.)
- **Groundwork for Brady i3300 support.** Not yet a working driver — this lands the
  supply-side foundation so the driver can follow without further catalog work:
  - A full "Brady i3300" supply catalog (B30/B33 series), covering paper, nylon, vinyl
    cloth, self-laminating vinyl wraps (Standard + High Strength adhesive), harsh-
    environment and all-weather polyester, FreezerBondz, PermaSleeve heat-shrink sleeves,
    raised panel, vinyl tape (All-Weather + Repositionable), magnetic tape, and ToughWash
    — around 150 real part numbers, sourced from Brady's own product pages.
  - Supplies can now record how many labels are arranged side-by-side on the physical
    roll ("Quantity per Row" in Brady's terms) — needed because some small B33 labels
    ship several-across on one roll width, and this can differ between two SKUs of the
    identical label size.

### Fixed
- **The first-launch setup no longer duplicates starter templates on every update.**
  Choosing "Install & Replace" for a starter template could silently create a second
  copy ("Sample 1_5x1_5-2", "-3", "-4"...) instead of overwriting the existing one — a
  side effect of the Engine no longer pre-loading the template list at launch (fixed
  last release to stop it stalling on Documents-folder permission). Existing
  duplicates from before this fix aren't merged automatically; remove the extras you
  don't want from the Template Designer's Open dialog or Finder.

### Changed
- **Dimension fields in the Designer's properties panel now show their unit in the
  header**, e.g. "Width (in)" / "Width (mm)" — matching the existing "(px)" convention
  for pixel-based fields. Applies to every position/size field (X, Y, Width, Height,
  Corner radius, Diameter, Radius, table Column width / Row height) and updates live
  when you switch units.

## [1.14.3] — 2026-07-18

### Fixed
- **Installer welcome screen no longer implies it installs starter templates.** It now
  says the optional component is the Vectorworks ConnectCAD plug-ins, and that starter
  templates and stock supply groups are offered by the app's first-launch setup — not the
  installer. No behavior change: the installer already never copied templates (that stopped
  in 1.10.0); only the wording was stale.

## [1.14.2] — 2026-07-18

### Changed
- **Maintenance release.** No functional changes from 1.14.1 — the same fixes,
  republished so an existing install can confirm it updates in place cleanly (the
  installer quits and relaunches the running apps, and the in-app updater offers the
  new version).

## [1.14.1] — 2026-07-18

### Fixed
- **Fresh installs no longer crash on first launch.** On a machine that wasn't the build
  machine, the Engine crashed the moment the first-launch supplies-and-templates window
  opened (the starter-template list looked for its resources in a location that only
  exists on a development machine). This is also why the Engine appeared to never
  auto-launch after the installer finished — it launched and quit within a second —
  and why the setup window then never came back: the one-time offer was consumed
  before the window survived. The resource lookup now uses the packaged location, the
  offer is only consumed after the window is actually up, and a CI check now blocks
  the crash-prone lookup pattern from ever returning.
- **The Engine no longer stalls at launch reading the Documents folder.** The menu-bar
  Engine used to scan the templates folder (inside your Documents folder) the instant it
  launched. On a fresh install that triggers the macOS "allow access to your Documents
  folder" permission, and while that was pending the Engine could freeze on launch. The
  Engine no longer touches Documents at startup at all; the first-launch setup window
  loads your existing templates in the background, so it always opens right away.
- **The installer no longer offers to install on Intel Macs it can't run on.** The apps
  are Apple-Silicon-only; the installer now says so up front instead of installing cleanly
  and then failing to launch.
- **Reinstalling over a running Engine now starts the new version.** Previously an in-place
  update could keep the already-running old Engine and show its (older) setup window; the
  installer now quits the running apps first so the freshly installed version takes over.
- **Clearer feedback if starter templates can't be saved.** If the templates folder can't
  be written (for example, Documents access was denied), the setup window now says so
  instead of closing as though everything installed.

## [1.14.0] — 2026-07-17

### Added
- **Reopen the first-launch setup any time.** Preferences ▸ Updates now has a
  **Set Up Supplies & Templates…** button that opens the stock-supply-groups and
  starter-templates window on demand. Installing from it is additive — existing supplies
  and templates aren't touched.

### Fixed
- **The first-launch setup window reliably appears on a fresh install.** The
  supplies-and-templates window could fail to show after the installer closed (it relied
  on a marker file written by the installer, and could sit behind the first-run update
  prompt). The app now detects a first run on its own, and shows the setup window before —
  not after — the update-settings prompt.
- **The menu-bar dropdown closes when you click elsewhere.** Clicking anywhere outside
  the Engine's menu now dismisses it — except while a job is actively printing, when it
  stays pinned so you can watch progress (the menu-bar button still hides/shows it any
  time). Previously it could stick open on top of other windows until toggled manually.

## [1.13.0] — 2026-07-16

### Fixed
- **Honest-progress rules now hold on every printer, in every window.** A conformance
  audit of the Engine↔driver handoff closed the remaining gaps: an M610 batch that wedges
  mid-job (jam, ribbon out) reports the real printed count instead of claiming all labels
  done; an M610 with an unreadable supply cell shows "unknown" while draining instead of a
  frozen counter; Brother P-touch printers now surface their own error reports (no media,
  cutter jam, cover open) as a failed job instead of "done"; pause/"unknown"/Cancel changes
  now reach the Custom Designer and Auto Print live during a print (previously only the
  menu bar updated); and a long M611 pause can no longer eat into the job's completion
  estimate after resume.
- **Brother "cut every label" jobs now show a per-label progress bar** — progress
  reporting is keyed to the printer's actual send strategy (the cut mode), not the
  one-at-a-time setting it ignores.
- **The calibration grid is sized from the loaded cassette's own reported printable area**
  when available, so it fits user-added or renamed supplies without a catalog match.

## [1.12.0] — 2026-07-16

### Added
- **Detect the loaded cassette from the menu bar.** Each printer row in the Engine's menu
  now has a detect button (↻) that re-reads the loaded supply on demand — the same action as
  the print window's "Detect supply" — with a spinner while the read runs. Handy right after
  swapping cassettes instead of waiting for the periodic re-scan.
- **The Engine now knows when you pause the M611 on the device.** Pausing mid-print shows
  **"Printer paused"** in the menu bar and the Custom Designer (instead of progress freezing
  or the job being marked done on a timer), and the job is held open — it resumes tracking
  when you resume the printer, completes only on the printer's real "complete" signal, and
  can still be cancelled while paused. Works in both one-label-at-a-time and full-job modes.
  (Discovered via live telemetry capture: the printer reports "Print Pausing"/"Print Paused"
  on the job itself.)

### Fixed
- **M611: wire wraps no longer print 90° off.** The auto-rotation added for raised panels
  (v1.9.0) guessed orientation from the label body's shape — and a square-bodied wrap like
  M6/BM-32-427 gave it nothing to go on, so it "corrected" the printer's already-correct
  rotation. Both Brady printers now fit the design against the **printable area rectangle
  the loaded cassette itself reports** (across-the-head × along-the-feed) — the definitive
  signal, confirmed against live cassette data for wraps and raised panels on both printers.
  Verified wire labels, panels, and continuous are all preserved; anything ambiguous keeps
  the printer's reported orientation.

### Changed
- **Auto-rotation never consults the supply catalog.** Print-time orientation now derives
  only from the label being printed and what the physically-loaded cassette reports about
  itself — never from catalog entries. Editing the supply library or adding custom supplies
  can no longer affect how existing labels orient on the printer.

## [1.11.0] — 2026-07-16

### Added
- **Launch the Engine at login.** A new toggle in **Preferences ▸ Advanced ▸ App Behaviour**
  starts the VectorLabel Engine automatically when you log in, so the menu-bar status and
  printing are ready without opening an app. macOS may ask you to approve it under System
  Settings ▸ General ▸ Login Items.
- **Each tab remembers its printer, and the right printer is picked for you.** In the Custom
  Designer and the Print window, every tab keeps its own printer selection. Opening a label
  file (or picking a template in the Print window) automatically selects a printer whose
  loaded supply matches — falling back to the printer you used most recently. A manual pick
  always wins and is never overridden.

### Fixed
- **M611: the printable area no longer flashes to 0 × 0.** A momentary partial status read
  from the printer could blank the supply readout and printable-area overlay for up to half
  a minute (often noticed right after changing printer settings). The Engine now keeps the
  last-known label geometry through such reads, so the printable area stays put.
- **M611: full-job prints start right away.** In full-job mode the printer waits for an
  end-of-job signal before feeding, and the Engine previously didn't send one until its
  status wait finished — so the physical print started roughly one estimated-print-time
  late. The end-of-job signal is now sent immediately after the job data (network and USB),
  and labels start feeding at once — verified on hardware.
- **Reprint from the Custom Designer now restores the full print setup.** Pressing Reprint
  on a Custom Designer print reopens the label with everything as it was when you printed:
  the print-range choice (All / Current / Selected / Range) and its bounds, which rows were
  ticked, the record shown in the preview, the database filter, sort, and search, and the
  printer — while still loading the current version of the label file (so later edits are
  kept). Previously the window reopened but snapped back to "All". Relatedly, an auto-sync
  refresh of the data file no longer resets your print selection mid-session.
- **M610: raised-panel labels no longer print rotated 90° off the panel.** The M610 now
  auto-orients each label to fit the loaded supply, the way the M611 already did — it checks
  the cassette's reported printable zone and rotates the design so it lands on the label the
  right way. This fixes square-bodied raised-panel supplies like M6-171-593, whose panel runs
  across the feed while the design canvas is authored the other way — verified on hardware.
  Hardware-verified wire wraps and continuous tape are untouched (the correction only applies
  where the loaded cassette's geometry can actually be disambiguated).
- **Brother P-touch text prints less bold, matching the on-screen preview.** The step that
  reduces the high-resolution render down to the printer's 180 dpi was biased toward keeping
  ink (to protect hairlines), which fattened every stroke edge so P-touch labels came out
  noticeably bolder than the preview. The Brother path now uses a neutral (true-stroke-width)
  ink threshold, so the printed weight tracks the preview — verified on hardware. (Brady
  M610/M611 are unchanged.)
- **Auto-scale now works together with word wrap.** Previously, turning on both "Wrap text"
  and "Auto-scale to fit" left the text at its full size — so wrapped text that needed more
  room than the box had was cut off. Now, when both are on, the text wraps *and* shrinks to
  the largest size at which every wrapped line fits inside the box, so nothing is clipped.
  Applies to text objects and table cells, in the designer preview, the print preview, and
  the printed label alike.

### Changed
- **The Engine shows "unknown" instead of guessing print progress.** When an M611 network
  printer stops reporting — or is paused on the device with labels sitting queued but not
  printing — the menu-bar job status (and the Custom Designer's print header) now shows a
  plain **"unknown"** rather than a made-up advancing count. A stalled job shows "unknown"
  for about its estimated print time, then is marked as printed. Progress is never faked.
- **Cancel appears only for jobs that can actually be cancelled.** A one-label-at-a-time
  print still shows a Cancel button. A full-job batch — a multi-label print sent in one shot
  because the printer is set to "full job" — can't be interrupted, so it no longer shows a
  Cancel button in the Engine menu or the Custom Designer.

### Known limitations
- **A physically paused M611 still can't be told apart from a slow one** — the printer
  reports the job as merely "queued", which we now surface honestly as "unknown". Detecting
  and labelling an actual pause is on the to-do list (needs the printer on hand to verify).

## [1.10.0] — 2026-07-13

### Added
- **Custom Designer: choose which worksheet (tab) to print from a multi-sheet Excel file.**
  When you bind an `.xlsx` that has more than one tab, a picker now asks which worksheet to
  use as the print data instead of silently taking the first one. To switch tabs later,
  right-click the data-file name (the button in the database bar) and choose **Redefine
  tab…** — it reopens the same picker with the current tab shown. The chosen tab is saved
  with the document, so reopening and "Refresh from source" re-read the same worksheet.
  Single-sheet workbooks and CSV files are unaffected (no picker).
- **Starter templates are offered when you first launch the suite.** The sample label
  templates now ship inside the app and appear on the first-launch setup screen (alongside
  the supply groups), where you choose which to install into your Templates folder.

### Changed
- **The installer no longer copies starter templates.** They're built into the app and
  offered on first launch instead, so a fresh install always has them available without the
  installer carrying a separate templates step.

### Fixed
- **The database grid keeps its position when you work in it.** Clicking a cell to edit,
  toggling a print checkbox, renaming a column header, or searching no longer moves the
  grid's scroll position — in both regular and free-edit modes.
- **The database header row stays visible while you scroll.** The column header row is now
  pinned to the top of the grid instead of scrolling out of view.
- **Wrapped text now stays inside its text box.** With "Wrap text" on, lines that didn't
  fit used to spill past the bottom of the box on the design canvas; they're now clipped to
  the box, matching what prints. (The print preview already behaved this way; the design
  canvas and the printed output now agree.)
- **Brother P-touch import: text comes in at the size P-touch shows, not larger.** P-touch
  shrinks text to fit a fixed frame, and the importer was reading the pre-shrink base size,
  so imported text landed oversized. It now reads the fitted size and turns on auto-scale
  for frames that shrink to fit, so imported labels match the original.

## [1.9.0] — 2026-07-08

> This batch is from a full senior code review (see `docs/reviews/2026-07-07-full-review.md`).
> Driver-timing fixes are marked **(needs hardware confirmation)** and should be soak-tested on a
> real printer. The auto-rotation behaviour shipped in 1.8.0 is unchanged.

### Security
- **Hardened the designer and print windows against malicious template/spreadsheet content.**
  A crafted template name, supply label, CSV filename, or printer name could previously inject
  markup into the app's windows; these are now escaped everywhere they're shown.

### Fixed
- **Imported labels now snap to a catalog supply.** A Brady `.BWT` matches the M6 group (by part
  number, then size) and a Brother `.lbx` matches the P-touch tape group; if nothing matches, the
  supply picker opens showing the imported label's dimensions so you can choose. This also fixes
  imported labels whose canvas orientation flipped as you clicked around.
- **Reprint reopens the Custom Designer exactly as you left it.** Pressing Reprint now restores the
  same label (the current version of the file if you've since edited it), the print range
  (All / Current / Selected / Range) and selected rows, and the printer that was chosen — instead of
  opening with defaults. (Applies to prints made from this version onward.)
- **M611: labels no longer print 90° off on back-to-back jobs (needs hardware confirmation).** The
  loaded cassette's orientation is now held stable across jobs instead of being re-read — sometimes
  wrongly — while the printer was still finishing the previous job.
- **Update window text no longer breaks mid-sentence.** The "What's new" release notes in the
  update popup (and the Preferences ▸ Updates card) now re-flow to the window width instead of
  keeping the changelog's source line breaks, so each item reads as one wrapping paragraph.
- **Inline text editing no longer destroys the object.** While editing a text box on the canvas,
  Backspace/Delete and the arrow keys now edit the text (and move the caret) instead of deleting
  or nudging the whole object.
- **Formatting edits are no longer silently lost.** Changing a single object's bold/size/colour/
  alignment/etc. now marks the document unsaved and can be undone — previously these edits didn't
  register as changes and vanished if you closed without an unrelated save.
- **A failed save now tells you.** If a template can't be written to disk, the app warns you and
  keeps the document marked unsaved, instead of showing "Saved" and quietly discarding your work.
- **Custom Designer: editing a record in the database pane** now marks the label unsaved.
- **Date/Time table cells survive save & reload** (they were being blanked on load).
- **Re-editing an imported photo** works from the original image again (brightness/contrast/
  threshold round-trip), and Template Designer saves keep the supply so a removed supply still
  renders at the right size.
- **Print window: replaced the broken file buttons.** Removed the non-working "Load CSV…" button;
  "+ Load template…" now opens a proper file picker and actually prints the template you choose —
  previously it could silently print a different design than the one shown.
- **Print preview matches the label better** — it now shows the template's own orientation
  (continuous and rotated die-cut) and applies letter-spacing, so the preview reflects what prints.
- **Excel dates import as dates**, not raw serial numbers like "46188".
- **No more crashes/hangs on bad input** — a malformed Brother `.lbx`, a corrupt spreadsheet cell
  reference, or a deeply-nested formula in an imported template are now handled gracefully.
- **Reprints and new exports that arrive while you're editing a template** are queued and shown
  when you finish, instead of being dropped.
- **Updates only install a verified download** — a failed/partial download can no longer be
  mistaken for a valid installer.
- **Suite settings and the supply catalog are now cross-process safe** — two apps editing at once
  no longer overwrite each other's changes, and a single bad read can't wipe your settings.
- **Driver reliability (needs hardware confirmation):** the M611 no longer reports a long batch
  as finished early (dropping the tail); the M610 waits for a batch to finish printing before
  releasing the USB connection; network printers can now be addressed by hostname, not just IP.
- Numerous smaller correctness/robustness fixes — FSEvents overflow rescans the full watched tree,
  CSV empty-row handling, print-queue ordering and folder-safety, and assorted preferences edges.

## [1.8.1] — 2026-07-06

### Fixed
- **Smoother middle-click panning.** Panning the design canvas with the middle mouse button no
  longer stutters — the scroll now updates once per animation frame instead of on every raw mouse
  event, so a high-report-rate mouse can't thrash the canvas.

## [1.8.0] — 2026-07-06

### Fixed
- **Brady die-cut labels auto-rotate to fit the loaded supply** (M611). At print time the engine
  now rotates whatever it's sent so it matches the printer's reported label orientation
  (across-head × feed) — so raised-panel labels (e.g. M6-173-593) that used to print sideways and
  clipped now fit. Correctly-oriented cassettes (wire labels) are unchanged; the rotate90 setting
  remains the manual override for square printable areas.
- **Loaded-cassette match ignores the ribbon-colour suffix.** A printer reporting the loaded
  material as e.g. `M6-173-593-BK` (the `-BK` = black ribbon) now matches the `M6-173-593`
  supply, instead of showing a false "⚠ mismatch" / size-mismatch prompt when the part and size
  actually agree.
- **Corrected the printable area of the 0.5"×1" wrap (M6-11-427)** in the default M6 catalog —
  its printable height is now 0.375" (was 0.25"). Existing catalogs are updated automatically on
  next launch, unless you've changed that supply's printable height yourself.
- **Supply-size edits now update the designer canvas instantly.** Changing a supply's
  width/height/printable size in the Engine's supply catalog editor is pushed to every open
  Template Designer, Custom Designer, and Auto Print window immediately (previously it could take
  up to ~2 seconds to appear). The canvas for the supply you're editing resizes in place.
- **Resize/rotate handles behave correctly when zoomed past 100%.** Dragging an object's corner
  handles (or the rotate / line-stretch handles, or a table's row/column dividers) while zoomed
  in no longer makes the object jump around the canvas — the live redraw now keeps the zoom scale
  applied during the drag.
- **Supply catalog fields apply when you click away.** Editing a size (or roll length / qty) in
  the supply catalog editor now captures the value as you type, so clicking elsewhere — even onto
  empty space — no longer discards the edit before Apply.
- **Clicking outside a text field now ends the edit in the Preferences windows.** In Preferences
  (and the Per-Printer Settings, Supply Catalog, and Supply Group editors), clicking anywhere off
  a field — including the "Add network printer" IP box — deselects it and commits the value,
  instead of leaving you stuck in the field.

### Added
- **Print just the current label** (Custom Designer). A new **Current** option next to
  All / Selected / Range prints only the record shown in the preview.
- **Supply list rows now show their part numbers.** Each supply in the catalog editor lists its
  part numbers on their own line under the type + count, wrapping to show them all within the tile.
- **Middle-mouse-button drag pans the design canvas** (like a hand tool). Hold the middle button
  and drag anywhere on the canvas to scroll around; the cursor becomes a closed hand while panning.

### Changed
- **Zoom keeps the center of the view fixed.** The designer's + / − zoom buttons now keep whatever
  was at the center of the canvas centered as you zoom in/out, instead of drifting off-screen.
  Reset returns to 100% and re-centers the label.
- **Simpler filter & sort in the Custom Designer.** The Source/Destination options (pair-sort
  modes and the "show both sides" filter) only apply to Vectorworks ConnectCAD wire data, so
  they're now hidden in the Custom Designer, which works on any CSV/Excel data.

### Fixed
- **Escape no longer closes the designer.** In the Template/Custom Designer, Escape now only
  deselects (or dismisses a menu/dialog) instead of closing the whole window — the Print window
  still closes on Escape.
- **Dragging a database column header now drops into the tab you're looking at** (Custom
  Designer). With more than one tab open, a header dragged onto the canvas could create the
  bound text field in a *different* tab, because a hidden background tab's web view was still
  intercepting the drop. Inactive tabs are now fully detached from the window (they can't
  receive the drop), and a drop that reaches a non-active tab is ignored — so the new field
  always lands on the tab you dragged into.

## [1.7.1] — 2026-07-04

### Added
- **"Set up supply groups" wizard.** It opens **automatically when an install finishes** — on a
  fresh install and on an in-place upgrade of the already-running Engine alike — and any time from
  Engine ▸ Preferences ▸ Printers ▸ **Set Up Supply Groups…**. The window lets you choose how to install the bundled
  supply groups. Each **available** group can be **Don't install**, **Install New**, or **Install
  & Replace** — it defaults to *Replace* when a group of the same name already exists, else
  *Install New* (and *Install New* over an existing name adds a numbered copy, e.g. "Brady M6 2").
  Your **existing** groups each get a **Delete** tick, and an **"Install all & clear existing"**
  preset wipes your groups and installs a clean factory set.

### Changed
- **Buy links are now an editable field per supply part**, instead of always sending you to a
  Brady part-number search. Brady (M6) parts come pre-filled with that same Brady search link
  (so nothing changes for them), and you can edit it or paste your own supplier URL in Engine ▸
  Preferences ▸ Printers ▸ Edit Supplies. Parts with a blank buy link — including Brother
  P-touch tapes for now — simply show no buy button.

## [1.7.0] — 2026-07-04

### Added
- **Keyboard shortcuts to save** in both designers: **⌘S** saves (the Custom Designer writes to
  the open label; the Template Designer saves the template), and **⌘⇧S** does Save As. While
  editing a template for the print window they map to Save & Return / Save As & Return.
- **Custom Designer start dialog.** When you open the Custom Designer (or click "+" for a new
  tab) it now offers your **5 most recent labels** to reopen, plus **Browse…** and **New blank
  label** — the same welcoming start the Template Designer has. Recents fill in as you open and
  save labels.
- **Metric or imperial units, suite-wide.** A new **Units** setting in the Engine's Preferences
  (Advanced ▸ Units) switches every app between **inches** and **millimetres** — the designer
  rulers, every dimension field, the print previews, and the supply readouts all follow, live.
  The Template/Custom Designer rulers also have a small **in/mm toggle in the top-left ruler
  corner** for a quick switch. Labels are always stored the same way, so switching units never
  changes a saved template.
- **Type fractions, other units, and math into any dimension field.** Enter values like `1/8"`,
  `1 1/4`, or `3mm` and they auto-convert to the field's unit; you can also do arithmetic, e.g.
  `.25"-1/8"` becomes `0.125"`. Works in inches or millimetres (`10+5` → 15 mm, and a comma
  decimal like `12,7` is accepted), across the designers' object/position/size/table fields and
  the supply editor.
- **Supply editor takes both units at once.** Every supply size now has an **inch field and a
  millimetre field** side by side — type into either and both update. Roll length shows **feet
  and metres** together. Handy when a supplier only lists one unit.
- **More shapes.** Rectangles gain a **corner radius** (in the object settings) for rounded
  rectangles; shapes (rectangle, ellipse, circle, and the new ones) gain a **solid-fill**
  option; and there are two new shape types — **triangle** and **polygon** (3–12 sides). They
  move, resize, and rotate like the existing shapes. Brother P-touch imports now bring these
  shapes across (rectangle, rounded rectangle, ellipse, polygon) instead of dropping them.
- **Date / Time text.** A text object, barcode, or table cell can now show the **current
  date and/or time**, chosen the same way as a data field — pick "Date/Time" and a format
  (date, time, or both) from presets. It renders the current date/time at print time.
  Formats now include the separator-less numeric ones **YYYYMMDD** (`20260704`),
  **MMDDYYYY** (`07042026`), and **DDMMYYYY** (`04072026`).
- **Header row by number** (Custom Designer data): the "first row is headers" tick is now a
  tick plus a **row number** (default 1) — set it higher to treat, say, row 10 as the header
  and hide everything above it. Works for CSV and Excel.
- **Auto-sync a bound data file** (Custom Designer): turn on **Auto-sync** and the data
  refreshes automatically whenever the source file changes. While it's on, in-app editing is
  hidden (the file drives the data), so your edits can't be overwritten mid-sync. The data
  toolbar shows an **"Auto-sync enabled · editing disabled — click to disable"** button while
  it's active, so it's clear why the edit controls are gone and how to get them back.

### Changed
- **Custom Designer database toolbar wraps neatly** on a narrow window — buttons now wrap in
  functional groups instead of getting cut off, with the left controls and right actions each
  staying justified to their side.
- **The data file is now a menu button** (like the Supply button): it shows the bound file's
  name (or "Choose data file" when none is bound). Click it (left or right) once a file is
  bound for a menu to **Replace file**, **Export**, or **Clear file** — replacing the separate
  Clear/Export toolbar buttons.
- **Each file dialog remembers its own last folder.** Choosing a data file, opening a custom
  label, saving, exporting, importing supplies, etc. each reopen where you last were for *that*
  action, instead of all sharing one location.

### Fixed
- **Opening a label no longer leaves an empty "Untitled" tab** (Custom Designer). Opening a file
  into a fresh blank tab now reuses that tab instead of stacking a stray untitled one beside it —
  and reopening a label that's **already open** simply switches to its existing tab (discarding
  the throwaway blank tab). Dismissing the start dialog on a new "+" tab (click-out or Escape)
  now cancels it and returns you to your previous tab, instead of leaving a blank one behind.
  A tab with unsaved changes is never reused or discarded.
- **"Save Label" now saves to the open file** (Custom Designer). It was always doing a Save As
  (prompting for a file every time); now it writes straight back to the open ".vlcus", and there's
  a separate **"Save as…"** button to save a copy to a new file. A brand-new label, or one opened
  from a Brady/Brother import, still prompts the first time (so an import is never overwritten).
- **"Text source" buttons no longer clip.** The Static / Field / Formula / Date-Time selector
  now wraps to two rows so "Formula" and "Date/Time" show in full on a narrow properties panel.
- **Records list keeps its scroll position.** Clicking a record to preview it no longer jumps
  the Custom Designer's data list back to the top.

## [1.6.2] — 2026-07-03

### Added
- **Save a problem report to a file.** The report popup now has a **Save Report…** button
  (alongside Send) that writes the full report to a Markdown file, so you can send it to the
  developer another way (e.g. an email attachment) instead of, or in addition to, submitting
  it. If a send fails, saving is offered too so the report is never lost.

## [1.6.1] — 2026-07-03

### Changed
- **Problem reports go through a relay, and include your contact details again.** The app no
  longer carries any GitHub token (a token shipped inside the app could be extracted from the
  installer). Reports are now sent to a small server-side relay that files the private issue,
  so the app ships **zero secrets**. Reports again include the reporter's name, email, and
  phone so the developer can follow up (reverting the 1.6.0 change that withheld them) —
  contact is still captured once and stored on your Mac.

## [1.6.0] — 2026-07-03

Hardening release from a full codebase + website audit — no new features, but a broad
set of correctness, safety, and privacy fixes.

### Fixed
- **Settings now apply across the whole suite.** Printer calibration offsets, the watch
  folder, print range and column/preset settings changed in one app (e.g. Engine
  Preferences) now reach the apps that actually render and print labels — previously each
  app kept its own private copy, so calibration silently did nothing on real prints.
  Existing settings are migrated automatically. Calibration also now applies correctly to
  network and Brother printers (not just USB Brady).
- **No lost prints or unsaved work at startup.** A print submitted just before the Engine
  finishes its first printer scan is now requeued and retried instead of silently failing;
  print failures are now announced (notification + a Recent Prints entry) rather than
  disappearing; and a minimized designer window (or a stray system window closing) can no
  longer make a designer quit without offering to save open tabs.
- **Security:** the print window now sanitizes template content the same way the designer
  does, closing a path where a malicious shared template could run code in the app.
- **Privacy:** problem reports temporarily withheld your name/email/phone from the report
  text. (Reverted in 1.6.1 — the private reports repo is meant to carry them for follow-up.)
- **Reliability:** a dead network printer can no longer freeze the Engine's status/scanning
  for minutes (bounded network writes); cassette reads no longer race the USB scan; a
  repeatedly-crashing preview no longer reload-loops; dropped file-system events during a
  burst are recovered by a rescan; and a re-export into an existing tab clears stale
  selection/search state so edits and deletes act on the right rows.
- Assorted smaller fixes: Vectorworks plugin exports write atomically, USB
  open-by-id skips a busy sibling printer, template reload can't drop a user file that
  happens to share an id, and several CI/release-workflow hardening fixes.

## [1.5.0] — 2026-07-02

### Added
- **Printer dropdowns show the loaded supply.** The printer selectors in the print
  window and the Custom Designer now append each printer's detected supply to its
  entry — the part number when the cassette reports one (e.g. "M611 — 12345 ·
  BM-109-427"), otherwise the loaded label size — so you can see what's in each
  printer before picking one.

### Changed
- **Cassette status stays fresh while idle.** The Engine now re-reads every idle
  printer's loaded cassette/supply every 30 seconds (previously the M610's SmartCell
  was only read on connect or a manual detect), and immediately when the print window
  opens or comes forward with a job. The sweep pauses entirely while anything is
  printing, so a refresh can never interfere with an active job.
- **Updates:** the update-available popup (and the Preferences ▸ Updates summary card)
  now lists the changes between your installed version and the new one — every version
  in between, straight from this changelog — instead of a general app summary. The
  GitHub release page for each version likewise shows that version's changelog section
  instead of boilerplate.

### Fixed
- **Print preview shows only the printable area again.** The print window's label
  preview (and expanded grid) no longer draw the physical label with hatched margins —
  on wrap supplies the dead space crowded out the label content. The hatched-margins
  view stays in the designers, where the physical context matters; the preview's
  "Printable area" row still notes when dimensions come from the loaded cassette.
- **Correct M611 USB id in the printer registry.** The default printer-model list
  recorded the Brady M611's USB product id as 0x010C (an early unverified guess);
  the real, hardware-confirmed id is 0x0013. Fresh installs now seed the correct id,
  and existing installs are migrated automatically (a hand-edited entry that already
  has the real id is left alone). M611 USB detection itself was never affected — the
  USB driver already matched the confirmed id — but the registry entry now agrees
  with the hardware, so per-printer settings resolve by id even for a renamed entry.

## [1.4.1] — 2026-07-02

### Changed
- **No more duplicate tabs.** Opening a file that's already open now switches to its
  existing tab instead of opening a second copy — in the Template Designer (.vltmp,
  whether opened from Finder, the Open… dialog, or the built-in template picker), the
  Custom Designer (.vlcus and not-yet-saved .BWT/.lbx imports), and the print window
  (a new export or a Reprint of a file that's already showing lands on its open tab).
  New/untitled documents and reprint-reopened designs are never deduplicated.
- **One shared suite log.** All four apps now write to a single rolling log file
  (~/Library/Logs/VectorLabel/VectorLabel.log, lines tagged per app) instead of one
  log per app, and error reports attach the combined suite timeline instead of a
  per-app log.

## [1.4.0] — 2026-07-02

### Added
- **Built-in error reporting.** When any of the four apps hits an error — a failed
  print, a file that won't open or save, a download/update failure, or a crash on the
  previous launch — the alert now offers **Report…**, which opens a popup where you can
  describe what happened and send the report privately to the developer (filed as a
  GitHub issue in a private repo). A **Report a Problem…** row in the Engine menu sends
  a report any time. The first report asks for your name, email, and (optionally) phone
  so the developer can follow up, then remembers them. Reports include app/version,
  macOS and hardware info, current printer status, and the app's recent log (each app
  now keeps a rolling log file under ~/Library/Logs/VectorLabel/).
- **Printable-area margins on the canvas.** Both designers and the print window's
  preview now show the label's physical edges with the unprintable margins hatched,
  so you can see exactly where the selected printer can print. In the Custom Designer
  and print window the margins come from the selected live printer (and its loaded
  cassette when it reports a printable area); the Template Designer — which has no
  printer attached — gains a **Printer dropdown** next to the Supply button to pick
  the target model, and the choice is saved with the template. A **Margins** toggle
  next to the grid control hides the overlay. P-touch margins come from the tape-width
  head table (e.g. 12 mm tape prints a centered ~9.9 mm band); Brady margins come
  from the supply catalog and live cassette telemetry.

## [1.3.1] — 2026-07-02

### Fixed
- **All four apps:** the blank "… Settings" window (an empty settings scene macOS 26
  presents when an app launches or activates) is now closed the instant it appears —
  on launch, after the installer relaunches the apps, on Dock/reopen, and around the
  update prompts. The 1.3.0 fix only covered the Engine's update prompts, which is why
  the window still opened on launch; Auto Print had the same stray window.

## [1.3.0] — 2026-07-02

### Changed
- **Updates:** the first-launch "How should VectorLabel check for updates?" prompt now
  defaults to **Every 7 days** (was: on every launch). Every option can still be chosen,
  and changed later in Preferences ▸ Updates.

### Fixed
- **Updates:** an empty "VectorLabel Engine Settings" window could appear when the update
  prompts surfaced (the first-launch question, "update available", "you're up to date",
  and update errors). It no longer does.

## [1.2.0] — 2026-07-01

### Added
- **Table object** in both designers: insert a grid of rows × columns, where every cell
  behaves like its own text box — static text, a data **field** (drag a column header
  onto a cell to bind it), or a **formula**, with full per-cell formatting incl.
  auto-scale. Select cells (shift = range, ⌘ = toggle), format or size many at once,
  copy/paste cells within or between tables, drag row/column lines to resize (with
  "Lock table size" on, drags redistribute inside the table), lock rows/columns to equal
  sizes, and right-click a cell to add/delete rows/columns or type an exact row height /
  column width. Double-click any cell to type into it directly. The first value entered
  into a cell (typed or bound) one-time auto-sizes its font to fit ~10 characters in the
  cell — after that the size is never changed automatically. Tables render identically
  in the designers, the print preview, and the printed output.
- **Auto-update from GitHub releases:** the Engine can now check GitHub for a newer
  VectorLabel — on every launch, every N days, or manually (a one-time prompt on first
  launch asks which; changeable any time in Preferences ▸ **Updates**, the new tab).
  When a newer version is found, a popup shows the release notes with **Update Now**
  (downloads the installer to ~/Downloads with progress, opens it, and quits the suite
  so it can be replaced cleanly), **Remind Me Tomorrow**, and **Don't Update** (skips
  that version only). The menu bar gains a "Check for Updates…" row, and Preferences ▸
  Updates shows the last-checked time plus a "Version X.Y.Z available" summary card —
  even for a skipped/snoozed version.
- **Online-only cloud files download before opening.** Files kept "online-only" by
  Dropbox, iCloud Drive, OneDrive or any similar sync service used to fail or stall when
  opened. Now every file the app opens — CSV/Excel data sources, templates, custom
  labels, Brady/Brother imports, images, supply-catalog imports, Finder double-clicks —
  first shows a small "Downloading …" popup with Cancel while the service fetches the
  file, then continues exactly where you left off. Cancel returns you to where you were.
- **Merged cells** in tables: select multiple cells and right-click → **Merge cells**
  (Excel-style bounding rectangle); right-click a merged cell → **Split cell** — the
  text stays in the top-left cell and every cell keeps the merged cell's formatting.
  Merges print identically in the preview and on the printer.
- **Clear commands** in tables: right-click any cell selection (single or multi) →
  **Clear text** (content only; formatting kept) or **Clear text & formatting**.

### Changed
- **Installer:** on macOS older than 14 (Sonoma) the installer now **warns** that the apps
  may not run correctly and lets you continue, instead of hard-blocking. (The apps target
  macOS 14 on Apple Silicon.)
- **Designers:** the stepper (▲/▼) buttons on numeric inputs in the object settings panel
  are bigger and easier to hit, and pressing ↑/↓ with a numeric input focused now steps
  and applies the value just like clicking the buttons.

### Fixed
- **Tables:** double-clicking a cell now reliably starts editing regardless of how the
  table was selected — and works for every cell type: static cells edit inline, formula
  cells open the formula editor, field cells jump to the column picker. (Editing engages
  by clicking the already-selected cell, so one click on an unselected table now selects
  the cell under the pointer and a second click — at any speed — starts editing.)

## [1.1.0] — 2026-07-01

First public release (open alpha).

### Added
- **The four-app suite:** VectorLabel Engine (menu-bar printing hub), Auto Print (the
  print window), Template Designer, and Custom Designer.
- **Design + print** wire / cable / asset / panel / patch labels on a true-to-size
  canvas — text, barcodes, QR, DataMatrix, images, symbols, lines and shapes.
- **Vectorworks ConnectCAD integration:** two export commands drop circuit data into a
  watch folder; the print window opens automatically with your records loaded.
- **Data binding & formulas:** bind a CSV or Excel (`.xlsx`) file (one label per row);
  spreadsheet-style formulas evaluate identically in preview and print.
- **Tabs everywhere:** the print window and both designers open several labels at once,
  with a `+` for new documents and per-tab live state.
- **Barcodes:** 15 linear + 2-D symbologies, rendered at each printer's native DPI.
- **Import:** open Brady `.BWT` and Brother P-touch `.lbx` templates (auto-converted
  into a new tab).
- **Printers:** Brady M610 & M611 (300 DPI) and Brother P-touch (180 DPI) over USB and
  the network, with live status/telemetry and cassette auto-detection on the M611.
- **Editable supply catalog** (sizes, part numbers, quantities, buy links) and
  **per-printer settings** (cut mode, orientation, calibration, feed-to-clear).
- **Signed + notarized installer** published from CI.

### Changed
- **Auto-scale text never truncates** — with auto-scale on, the font shrinks until the
  whole value fits; it no longer clips to a "…".

### Fixed
- The light / dark / auto **appearance choice relays across the whole suite.** Changing it
  from the Engine menu (or Preferences) immediately switches Auto Print and both designers
  too; an app opened later syncs to the current setting on launch.

### Known limitations (open alpha)
- The Brady **M611** is hardware-validated. The Brady **M610 cut** behavior and the
  **Brother P-touch** drivers are built but **not yet hardware-confirmed** — see
  [`docs/PTOUCH-DRIVER-STATUS.md`](docs/PTOUCH-DRIVER-STATUS.md).

[Unreleased]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/compare/v1.8.1...HEAD
[1.8.1]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.8.1
[1.8.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.8.0
[1.7.1]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.7.1
[1.7.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.7.0
[1.6.2]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.6.2
[1.6.1]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.6.1
[1.6.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.6.0
[1.5.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.5.0
[1.4.1]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.4.1
[1.4.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.4.0
[1.3.1]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.3.1
[1.3.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.3.0
[1.2.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.2.0
[1.1.0]: https://github.com/Cooper-Audio-Services/VectorLabel-Releases/releases/tag/v1.1.0
