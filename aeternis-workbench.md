# Aeternis — Clinician Workbench (clickable prototype)
*genre:* `design-draft` · *route:* `/aeternis-workbench`

A clickable prototype of the Aeternis product. Eight working sections in
  four groups that mirror the solution architecture (Devices & sync =
  ingestion + time sync; Pipeline = the whole layer live; Engine & releases
  = annotation engine + model registry; Audit = audit & de-identification).
  The clinical sections:
  Review (a synced timeline of one bed with the annotations the context
  layer proposed; confirm, correct or reject each one in a tap or a key),
  Live (the bedside waveforms sweeping in real time with an event stream),
  Quality (how often clinicians agree with the engine, review time,
  confidence calibration) and Exports (the EMR feed and de-identified
  training snapshots). Every bed in the sidebar opens. All patients,
  hospitals and values are synthetic and generated on this page.

## Components

### `Masthead`

**Role:** panel

Masthead shared by the four Aeternis pages: product mark, the kit's
       navigation, and a controlled-document block (document id, revision,
       date, status) the way medical-device documentation is headed.
       Also loads the kit's typefaces, IBM Plex Sans / Condensed / Mono.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    <div>
      "Æ"
    <div>
      <div>
        "Aeternis"
      <div>
        "Clinical context layer"
  <div>
    {… .map →}
    <BlockStatement>
  <div>
  <div>
    <span>
      "Document"
    <span>
      {docId}
    <span>
      "Revision"
    <span>
      "C, 15 Oct 2026"
    <span>
      "Status"
    <span>
      "Draft for discussion"
```

</details>

### `Vitals`

**Role:** compute

Deterministic synthetic vitals for one bed over the 30-minute
       window. Artifacts are produced from the bed's own annotation windows,
       so bands, curves, hover values and the detail card always agree.

<details><summary>JSX outline</summary>

```
<Identifier>
```

</details>

### `Icon`

**Role:** chip

Stroke icon drawn from the ICONS table, sized in px; the only icon
       source in the app, so every glyph has the same weight.

<details><summary>JSX outline</summary>

```
<Diagram>
  {… .map →}
  <path>
```

</details>

### `KindPill`

**Role:** chip

Annotation-kind pill; each kind owns one colour across the app.

<details><summary>JSX outline</summary>

```
<span>
  <span>
  {k.label}
```

</details>

### `StatusPill`

**Role:** chip

Review status: needs review, confirmed, corrected or rejected.

<details><summary>JSX outline</summary>

```
<span>
  {label}
```

</details>

### `Confidence`

**Role:** chip

Confidence meter: a short track filled to the confidence, plus the value.

<details><summary>JSX outline</summary>

```
<span>
  <span>
    <span>
  <span>
    {conf.toFixed(…)}
```

</details>

### `Card`

**Role:** chip

A dark card surface used by every panel inside the app.

<details><summary>JSX outline</summary>

```
<div>
  {children}
```

</details>

### `Eyebrow`

**Role:** chip

Small uppercase section label inside cards.

<details><summary>JSX outline</summary>

```
<div>
  {children}
```

</details>

### `BrowserBar`

**Role:** panel

Browser window bar with the product URL, so the prototype reads as
       a real web app rather than a drawing.

<details><summary>JSX outline</summary>

```
<div>
  {… .map →}
  <span>
  <div>
    <div>
      <Icon name="lock">
      <span>
        "app.aeternis.health"
        <span>
          "/icu-3/bed-"
          {bed}
          "/"
          {tab}
  <button type="button" title={…}>
    <Icon name={…}>
    {full ? … : …}
    "Exit · Esc"
    "Full screen"
```

</details>

### `EnvStrip`

**Role:** chip

Thin environment strip under the browser bar, the way clinical
       software marks a non-production instance.

<details><summary>JSX outline</summary>

```
<div>
  <span>
    "Demo environment"
  <span>
    "Synthetic patients and values · ICU 3 pilot configuration · release rules-0.4.2 · not for clinical use"
```

</details>

### `Sidebar`

**Role:** panel

Left sidebar: product mark, unit switcher, the eight sections in four groups, every
       bed of the unit with its review backlog, and the signed-in user.
       Sections and beds are all live buttons.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    <div>
      "Æ"
    <div>
      <div>
        "Aeternis"
      <div>
        "Clinical context"
  <div>
    <div>
      <div>
        "ICU 3 · Pilot hospital"
      <div>
        "8 beds · on-prem"
    <Icon name="chevron">
  <div>
    {… .map →}
    <BlockStatement>
  <div>
    <Eyebrow>
      "Beds"
  <div>
    {… .map →}
    <BlockStatement>
  <div>
    <div>
      "RT"
    <div>
      <div>
        "Rachel Tan, RN"
      <div>
        "Reviewer · day shift"
    <Icon name="settings">
```

</details>

### `TopBar`

**Role:** panel

Top bar of the main area: breadcrumb, global search, device sync
       state, hospital clock and notifications.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    "ICU 3"
    <span>
      "/"
    "Bed"
    {bed}
    <span>
      "/"
    <span>
      {label}
  <div>
  <div>
    <Icon name="search">
    <span>
      "Search patients, beds, annotations"
    <span>
      "⌘K"
  <div>
    <span>
    "14 devices synced · drift &lt; 20 ms"
  <div>
    "10:20:04"
    <span>
      "SGT"
  <div>
    <Icon name="bell">
    <span>
```

</details>

### `PatientHeader`

**Role:** panel

Patient header for the open bed: de-identified id, context, devices,
       and monitor-style current numerics in their conventional colours.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    {bed.id}
  <div>
    <div>
      "Patient"
      {bed.patient}
    <div>
      {bed.meta}
      <span>
        "·"
      <span>
        <Icon name="shield">
        "de-identified view"
      <span>
        "·"
      "IntelliVue MX800 · 2 × Alaris · Hamilton C6"
  <div>
  {… .map →}
  <div>
    <div>
      {k}
    <div>
      {v}
    <div>
      {u}
```

</details>

### `Timeline`

**Role:** node

Synced multi-track timeline for one bed. Annotation bands span all
       tracks; hovering shows a crosshair with every value at that second;
       clicking anywhere inside a band opens that annotation.

<details><summary>JSX outline</summary>

```
<Diagram id="timeline">
  {…}
  {… .map →}
  <g>
    <line>
    <text>
      {hms(…).slice(…)}
  {…}
  {… .map →}
  <BlockStatement>
  {…}
  {… .map →}
  <BlockStatement>
  {…}
  {anns.some(…) && …}
  <g>
    <line>
    <text>
      "EMR charted 10:15"
    <text>
      "true start 10:01:32"
  {…}
  {hoverRow && …}
  <g>
    <line>
    <rect>
    <text>
      {hms(…)}
    {… .map →}
    <BlockStatement>
  {…}
  <rect>
```

</details>

### `Detail`

**Role:** panel

The selected annotation: kind, time, finding, confidence, the
       engine's reason, its sources, what confirming changes — and the
       actions. Correct opens the list of alternative labels.

<details><summary>JSX outline</summary>

```
<Card>
  <div>
  <div>
    <div>
      <KindPill>
      <div>
      <StatusPill>
    <div>
      <div>
        {ann.title}
      <div>
        <Icon name="clock">
        {hms(…)}
        {… ? … : …}
        <TemplateLiteral>
        " · exact"
    <div>
      {ann.value}
    <div>
      "Engine confidence"
      <Confidence>
    <div>
      <Eyebrow>
        "Why the engine thinks so"
      <div>
        {ann.reason}
      <div>
        {… .map →}
        <span>
          {s}
    {… ? … : …}
    <div>
      <span>
        "On confirm ·"
      {ann.effect}
    <div>
      <Eyebrow>
        "What actually happened?"
      {… .map →}
      <button type="button">
        <span>
          {… && …}
          <span>
        {o}
    {… ? … : …}
    <div>
      <button type="button">
        <Icon name="check">
        "Confirm"
      <button type="button">
        <Icon name="edit">
        "Correct"
      <button type="button">
        <Icon name="x">
        "Reject"
    <div>
      <button type="button">
        "Save correction"
      <button type="button">
        "Cancel"
    <div>
      {… .map →}
      <span>
        <span>
          {kk}
        {l}
```

</details>

### `Queue`

**Role:** panel

Review queue for the open bed with filter tabs; each row selects
       the same annotation the timeline bands do.

<details><summary>JSX outline</summary>

```
<Card>
  <div>
    <div>
      "Review queue"
    <div>
      {… .map →}
      <button type="button">
        {l}
        <span>
          {counts.id}
    <div>
    <div>
      "Sorted by time · window 09:50–10:20"
  <div>
    {… .map →}
    <Eyebrow>
      {h}
  {… && …}
  <div>
    "No annotations in this view."
  {… .map →}
  <BlockStatement>
```

</details>

### `ReviewView`

**Role:** panel

The Review section: patient header, timeline with detail card, the
       queue, and the three outputs of the review. Owns keyboard shortcuts.

<details><summary>JSX outline</summary>

```
<div>
  <PatientHeader>
  <div>
    <Card>
      <div>
        <div>
          "Synced timeline"
        <div>
          "4 devices on one clock · hover for values, click a band to inspect"
        <div>
        {… .map →}
        <span>
          {r}
      <Timeline>
    <Detail>
  <Queue>
  <div>
    {… .map →}
    <Card>
      <div>
        <Icon name={ic}>
      <div>
        <Eyebrow>
          {k}
        <div>
          {v}
        <div>
          {s}
```

</details>

### `EmptyBed`

**Role:** panel

Empty state for a bed with no patient or no device feed.

<details><summary>JSX outline</summary>

```
<Card>
  <div>
    <div>
      <Icon name="pulse">
    <div>
      "No patient on this bed"
    <div>
      "Devices are idle. The bed reappears in review when a feed starts."
```

</details>

### `Waveforms`

**Role:** animated-region

Bedside waveforms sweeping like a monitor: four traces drawn from
       synthetic beat shapes, erased just ahead of the sweep line.

<details><summary>JSX outline</summary>

```
<Diagram id="waves">
  {… .map →}
  <BlockStatement>
```

</details>

### `LiveView`

**Role:** panel

The Live section: monitor-style sweeping waveforms with big
       numerics, and the stream of annotations the engine is proposing now.

<details><summary>JSX outline</summary>

```
<div>
  <PatientHeader>
  <div>
    <Card>
      <div>
        <span>
        <span>
          "Live · Bed"
          {bed.id}
        <span>
          "25 mm/s · tapped copy of the concentrator feed · read-only"
      <div>
        <div>
          <Waveforms>
        <div>
          {… .map →}
          <div>
            <div>
              <span>
                {w.label}
              <span>
                {… ? … : …}
                <TemplateLiteral>
                <MemberExpression>
            <div>
              {w.value(…)}
            <div>
              {w.unit}
    <Card>
      <div>
        <div>
          "Engine · live proposals"
        <span>
          "Streaming"
      {… .map →}
      <div>
        <div>
        <div>
          <div>
            <span>
              {title}
            <span>
              {tm}
          <div>
            {sub}
          <div>
            <Confidence>
      <div>
        "Proposals below 0.75 confidence wait for a reviewer; above it they are pre-filled and need one tap."
```

</details>

### `QualityView`

**Role:** panel

The Quality section: KPIs, clinician agreement per annotation kind,
       review time trend and confidence calibration — the evidence that
       the engine's labels can be trusted.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    <div>
      "Annotation quality · ICU 3"
    <div>
      "Last 14 days · 8 beds · 11 reviewers · evaluated against clinician decisions"
  <div>
    {… .map →}
    <Card>
      <Eyebrow>
        {k}
      <div>
        {v}
      <div>
        {s}
  <div>
    <Card>
      <div>
        "Clinician agreement by kind"
      <div>
        "Share of proposals confirmed without change"
      {… .map →}
      <div>
        <div>
          <span>
            {KIND.kind.label}
          <span>
            <b>
              {Math.round(…)}
              "%"
            "·"
            {n.toLocaleString(…)}
            "labels"
        <div>
          <div>
          <div>
      <div>
        "White tick = 85% target. Bedside care is inferred without cameras in the MVP."
    <Card>
      <div>
        "Median review time per label"
      <div>
        "Seconds · falls as reviewers trust the engine"
      <Diagram id="review-time">
        {… .map →}
        <BlockStatement>
        <polygon>
        <polyline>
        {… .map →}
        <circle>
        {… .map →}
        <text>
          {l}
        <text>
          "3.4 s"
    <Card>
      <div>
        "Confidence calibration"
      <div>
        "Stated confidence vs observed agreement"
      <Diagram id="calibration">
        <line>
        <line>
        <line>
        {… .map →}
        <BlockStatement>
        <text>
          "stated 0.5 → 1.0"
        <text>
          "observed"
      <div>
        "Points on the diagonal: a 0.9 means 9 in 10."
  <div>
    <Card>
      <div>
        "Most frequent corrections"
        <span>
          "· each one becomes a rule change"
      {… .map →}
      <div>
        <span>
          {from}
        <span>
          "→"
        <span>
          <span>
          {to}
        <span>
          {n}
          "×"
        <span>
          {fix}
    <Card>
      <div>
        "Backlog by bed"
      <Diagram id="backlog">
        {… .map →}
        <BlockStatement>
      <div>
        "Open proposals older than 1 h · amber above 6"
```

</details>

### `ExportsView`

**Role:** panel

The Exports section: the live EMR feed, the de-identified training
       snapshots (a new one can be created here), and the privacy checks
       each snapshot passes before it may leave the hospital.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    <div>
      <div>
        "Exports"
      <div>
        "Two outputs, never mixed: standard data to the EMR, annotated de-identified data for training"
    <button type="button">
      <Icon name="plus">
      "Create training snapshot"
  <div>
    {… .map →}
    <Card>
      <div>
        <Icon name={ic}>
      <div>
        <div>
          <span>
            {k}
          <span>
            {v}
        <div>
          {s}
  <div>
    <Card>
      <div>
        "Training snapshots"
      <div>
        {… .map →}
        <Eyebrow>
          {h}
      {… .map →}
      <div>
        <span>
          {r.v}
        <span>
          {r.date}
        <span>
          {r.labels.toLocaleString(…)}
        <span>
          {r.beds}
        <span>
          {r.size}
        <span>
          {pill(…)}
        <span>
          <button type="button">
            <Icon name="download">
            "Manifest"
    <Card>
      <div>
        "Checks before data leaves"
      {… .map →}
      <div>
        <span>
          <Icon name="check">
        {c}
  <Card>
    <div>
      "Activity"
    {… .map →}
    <div>
      <span>
        {tm}
      <span>
        <span>
        {who}
      <span>
        {what}
```

</details>

### `ViewHeader`

**Role:** panel

Title row used by every section: name, one-line context, the
       architecture component(s) it shows, and optional actions.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    <div>
      <div>
        {title}
      {arch && …}
      <CallExpression>
    <div>
      {sub}
  {children}
```

</details>

### `GhostButton`

**Role:** chip

Secondary action button in the dark UI.

<details><summary>JSX outline</summary>

```
<button type="button">
  {icon && …}
  <Icon name={icon}>
  {children}
```

</details>

### `Kpi`

**Role:** chip

KPI tile: label, value, sub-line; optional accent colour.

<details><summary>JSX outline</summary>

```
<Card>
  <Eyebrow>
    {k}
  <div>
    {v}
  <div>
    {s}
```

</details>

### `DevicesView`

**Role:** panel

Devices & sync: every device feeding the edge box, its driver,
       clock offset before and after time sync, message rate and a decoded
       sample of what it sends. Mirrors "Device ingestion" and "Time sync &
       normalisation" on the architecture.

<details><summary>JSX outline</summary>

```
<div>
  <ViewHeader title="Devices & sync">
    <GhostButton>
      "Resync clocks"
    <GhostButton>
      "Add device"
  <div>
    <Kpi>
    <Kpi>
    <Kpi>
    <Kpi>
  <div>
    <Card>
      <div>
        {… .map →}
        <Eyebrow>
          {h}
      {… .map →}
      <div>
        <span>
          {x.bed}
        <span>
          <span>
          {x.kind}
        <span>
          {x.model}
        <span>
          {x.link}
        <span>
          {… ? … : …}
          "+"
          ""
          {x.raw}
          "ms"
        <span>
          "±"
          {x.after}
          "ms"
        <span>
          {x.rate}
        <span>
          {x.last}
    <div>
      <Card>
        <div>
          "One clock for every device"
        <div>
          "Raw device clock offset (amber) → after sync (teal)"
        <Diagram id="clock-offsets">
          <line>
          {… .map →}
          <g>
            <line>
            <circle>
          {… .map →}
          <text>
            {… ? … : …}
            "0"
            <TemplateLiteral>
      <Card>
        <Eyebrow>
          "Decoded · bed"
          {d.bed}
          "·"
          {d.kind.toLowerCase(…)}
        <div>
          {d.model}
        <div>
          {SAMPLE.d.kind.join(…)}
        <div>
          "Clock"
          {… ? … : …}
          "fast"
          "slow"
          "by"
          {Math.abs(…)}
          "ms → corrected to ±"
          {d.after}
          "ms."
```

</details>

### `PipelineView`

**Role:** animated-region

The architecture's data path as a live view: the same seven
       components from ingestion to outbound, in their edge box and core
       server, with dots moving through every link and each stage's health.

<details><summary>JSX outline</summary>

```
<div>
  <ViewHeader title="Pipeline">
    <span>
      <span>
      "All stages healthy"
  <Card>
    <div>
    <div>
    <div>
      <Eyebrow>
        "Edge box · ICU 3"
    <div>
      <Eyebrow>
        "Core server · on-prem"
    <div>
      <Diagram id="pipe-links">
        {… .map →}
        <polyline>
        {LINKS.flatMap(…)}
    {… .map →}
    <div>
      <div>
        <span>
        <span>
          {s.name}
      <div>
        {s.where}
      <div>
        {s.m1}
      <div>
        {s.m2}
  <div>
    {… .map →}
    <Card>
      <div>
        <span>
          {k}
        <span>
          {spec}
      {… .map →}
      <div>
        <span>
          {n}
        <div>
          <div>
        <span>
          {Math.round(…)}
          "%"
      <div>
        {foot}
    <Card>
      <div>
        "Two outputs, never mixed"
      {… .map →}
      <div>
        <div>
          <span>
            {k}
          <span>
            {n}
        <div>
          {v}
```

</details>

### `EngineView`

**Role:** panel

Engine & releases: the active signed release, every label with its
       method, reference-set precision / recall, threshold and mode (auto,
       review, shadow — switchable), and the release history with rollback.
       Mirrors "Annotation engine" and "Model registry" on the architecture.

<details><summary>JSX outline</summary>

```
<div>
  <ViewHeader title="Engine & releases">
    <GhostButton>
      "Evaluation report"
  <Card>
    <div>
      <Icon name="shield">
    <div>
      <Eyebrow>
        "Active release"
      <div>
        {active}
      <div>
        "Signed by Hygge · signature and checksum verified on install · 7 labels · rules-first, 1 model in shadow"
    {… .map →}
    <div>
      <Eyebrow>
        {k}
      <div>
        {v}
  <Card>
    <div>
      <span>
        "Labels"
      <span>
        "Auto: written without review · Review: pre-filled, one tap · Shadow: computed, compared, not shown"
    <div>
      {… .map →}
      <Eyebrow>
        {h}
    {… .map →}
    <div>
      <span>
        {r.id}
      <span>
        {r.name}
      <span>
        <KindPill>
      <span>
        {r.method}
      <span>
        {r.p.toFixed(…)}
      <span>
        {r.r.toFixed(…)}
      <span>
        "≥"
        {r.th.toFixed(…)}
      <span>
        {… .map →}
        <button type="button">
          {m}
  <div>
    <Card>
      <div>
        "Release history · model registry"
      {… .map →}
      <BlockStatement>
    <Card>
      <div>
        "How a release reaches this hospital"
      {… .map →}
      <div>
        <span>
          {…}
        <div>
          <div>
            {k}
          <div>
            {v}
```

</details>

### `AuditView`

**Role:** panel

Audit: an immutable log of who saw, labelled or exported what, with
       filters, plus roles and the data-access policy. Mirrors "Audit,
       access control & de-identification" on the architecture.

<details><summary>JSX outline</summary>

```
<div>
  <ViewHeader title="Audit">
    <GhostButton>
      "Export audit log"
  <div>
    <Card>
      <div>
        {… .map →}
        <button type="button">
          {l}
      <div>
        {… .map →}
        <Eyebrow>
          {h}
      {… .map →}
      <div>
        <span>
          {r.0}
        <span>
          {r.2}
        <span>
          {r.3}
        <span>
          {r.4}
        <span>
          {r.5}
    <div>
      <Card>
        <div>
          "Roles"
        {… .map →}
        <div>
          <div>
            <div>
              {k}
            <div>
              {v}
          <span>
            {n}
      <Card>
        <div>
          "Data-access policy"
        {… .map →}
        <div>
          <span>
            <Icon name="check">
          {c}
```

</details>

### `App`

**Role:** layout

The app window itself. Inline it is a 1520-px browser window on the
       canvas; in full screen it fills the viewport and the main area
       scrolls on its own. All state comes from AppHost, so switching
       between the two keeps the open section, bed and review decisions.

<details><summary>JSX outline</summary>

```
<div>
  <BrowserBar>
  <EnvStrip>
  <div>
    <Sidebar>
    <div>
      <TopBar>
      <div>
        {… && …}
        <ReviewView>
        {… && …}
        <LiveView>
        {… && …}
        <QualityView>
        {… && …}
        <ExportsView>
        {… && …}
        <DevicesView>
        {… && …}
        <PipelineView>
        {… && …}
        <EngineView>
        {… && …}
        <AuditView>
  {toast && …}
  <div>
    <span>
      <Icon name="check">
    {toast.msg}
```

</details>

### `AppHost`

**Role:** animated-region

Owns the prototype's state (section, bed, review decisions, toast)
       and where it is shown: inline on the canvas, or in full screen —
       a fixed layer over the whole page via a portal, plus the browser's
       Fullscreen API when the frame allows it. Esc or the button returns.

<details><summary>JSX outline</summary>

```
<Box id="app">
  {full ? … : …}
  <div>
    "The prototype is open in full screen · press Esc to come back"
  <App>
  {full && …}
  <CallExpression>
  {… && …}
  <FullScreenButton>
```

</details>

### `FullScreenButton`

**Role:** chip

The floating "Open full screen" button pinned to the top-right
       corner of the inline prototype.

<details><summary>JSX outline</summary>

```
<button type="button">
  <Icon name="expand">
  "Open full screen"
```

</details>

### `Heading`

**Role:** panel

Title above the prototype: what it is, how to use it, and that the
       data is synthetic.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    "Clinician Workbench"
  <div>
    "Eight sections in four groups, named after the components of the solution architecture: Clinical (Review, Live monitor), Data (Devices &amp; sync, Pipeline), Models (Engine &amp; releases), Governance (Quality, Exports, Audit). Every section, bed and button works. On Review, hover the timeline, click a band, then Confirm / Correct / Reject (or press C, R, ↓). Patients, hospital and values are synthetic."
```

</details>

### `AeternisWorkbench` — default export

<details><summary>JSX outline</summary>

```
<Scene>
  <div>
    <Masthead>
    <Heading>
    <AppHost>
```

</details>
