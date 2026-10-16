# Aeternis — how the system fits into a hospital
*genre:* `network-graph` · *route:* `/aeternis-system`

The clinical context layer sits beside the existing bedside → central
  station → EMR path and never replaces it. It taps a copy of the bedside
  feed, puts every device on one clock, annotates the data, lets a
  clinician confirm the labels, and sends two outputs: the standard feed
  to the EMR and time-exact annotated data to the training store. Models
  are trained outside the hospital on de-identified data only and come
  back as signed releases. Solid boxes are the MVP; dashed boxes come
  after it.

  Data moves on the page: dots run along every live edge. "Follow one
  annotation" walks a norepinephrine start through the eight steps from
  the infusion pump to a signed model release, lighting only the boxes
  and edges of the current step. "AI" lights the four places where AI
  runs and says what each one does.

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

### `Node`

**Role:** node

One component card. `kind` sets the look: `mvp` (built in the MVP),
       `later` (dashed, after MVP), `existing` (hospital's own system, grey).

<details><summary>JSX outline</summary>

```
<Box id={id}>
  {… && …}
  <span>
    "AI"
  <div>
    {icon && …}
    <span>
      {icon}
    <div>
      {title}
    {later && …}
    <span>
      "after MVP"
  {sub && …}
  <div>
    {sub}
```

</details>

### `Zone`

**Role:** layout

A titled zone (hospital network, partner environment, the layer
       itself). The border style says whose infrastructure it is.

<details><summary>JSX outline</summary>

```
<Box id={id}>
  <div>
    <div>
      {title}
    {note && …}
    <div>
      {note}
  {children}
```

</details>

### `Header`

**Role:** panel

Page header with three facts a hospital IT reviewer asks first.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    "A context layer beside the EMR, not instead of it"
  <div>
    "The hospital keeps its monitors, concentrators and EMR. The layer taps a copy of the bedside feed, adds context and clinician-confirmed labels, and sends two outputs: the standard feed to the EMR and time-exact annotated data to the training store."
  <div>
    {fact(…)}
    {fact(…)}
    {fact(…)}
    {fact(…)}
```

</details>

### `AuditBar`

**Role:** chip

Cross-cutting strip on top of the core: audit, access control and
       de-identification wrap every component rather than sitting in the flow.

<details><summary>JSX outline</summary>

```
<Box id="n-audit">
  <span>
    "⛨"
  <b>
    "Audit, access control & de-identification"
  <span>
    "wrap every component · SYNAPSE / PDPA / GDPR"
```

</details>

### `Hospital`

**Role:** layout

The hospital network: bedside devices, the concentrator, the
       existing central-station → EMR path on top, and the context layer
       (edge + core) beneath it, with clinicians on the right.

<details><summary>JSX outline</summary>

```
<Zone id="zone-hospital" title="Hospital network">
  <div>
    {…}
    <Zone id="zone-bedside" title="Bedside · per bed">
      <Group>
        <Node id="n-monitor" title="Patient monitor">
        <Node id="n-pumps" title="Infusion pumps">
        <Node id="n-vent" title="Ventilator">
        <Node id="n-sensor" title="Room sensor">
        <Node id="n-voice" title="Nurse voice">
    {…}
    <div>
      <Node id="n-conc" title="Bedside concentrator">
    {…}
    <div>
      <div>
        <Node id="n-central" title="Central station / MDI">
        <div>
          "Values arrive in the EMR averaged into 5–15 min blocks; interventions are charted 5–15 min late. This is the gap the layer closes."
      <Zone id="zone-layer" title="Aeternis · Clinical context layer">
        <div>
          <Zone id="zone-edge" title="Edge box · per unit">
            <Group>
              <Node id="n-ingest" title="Device ingestion">
              <Node id="n-sync" title="Time sync & normalisation">
              <Node id="n-buffer" title="Local buffer">
              <Node id="n-pose" title="Pose & activity detector">
          <Zone id="zone-core" title="Core">
            <AuditBar>
            <div>
              <Node id="n-store" title="Time-series store">
              <Node id="n-out" title="Outbound adapters">
              <Node id="n-engine" title="Annotation engine">
              <div>
              <Node id="n-review" title="Review workbench">
    {…}
    <div>
      <Node id="n-emr" title="EMR">
      <Node id="n-clin" title="Clinicians">
```

</details>

### `Partner`

**Role:** layout

The partner environment in the EU where de-identified data becomes
       labelled datasets, models are trained and evaluated, and signed
       releases go back to the hospital's annotation engine.

<details><summary>JSX outline</summary>

```
<Zone id="zone-partner" title="Partner environment · EU">
  <div>
    <Node id="n-registry" title="Model registry">
    <Node id="n-training" title="Training & evaluation">
    <Node id="n-dataset" title="Labelled dataset">
    <Node id="n-train-store" title="AI training store">
```

</details>

### `StoryBar`

**Role:** panel

The control strip above the diagram: follow one annotation (play,
       pause, step chips), the AI view and the dot flow switch, plus the
       caption of what is lit right now and the data it carries.

<details><summary>JSX outline</summary>

```
<Box id="story">
  <div>
    <button type="button">
      <span>
        {playing ? … : …}
        "❚❚"
        "▶"
      {playing ? … : …}
      "Pause"
      <ConditionalExpression>
    <div>
      <button type="button">
        "Overview"
      {… .map →}
      <button type="button" title={st.title}>
        {…}
    <div>
    <button type="button">
      <span>
        "✦"
      "AI"
    <button type="button">
      <span>
      "Data flow"
      {flow ? … : …}
      "on"
      "off"
  <div>
    {cur && …}
    <div>
      <div>
        "Step"
        {…}
        "of"
        {STEPS.length}
      <div>
        {cur.title}
      <div>
        {cur.text}
    <div>
      <div>
        "Data at this step"
      {cur.packet}
    {… && …}
    <div>
      {… .map →}
      <div>
        <div>
          {k}
        <div>
          {v}
    {… && …}
    <div>
      <b>
        "Data is moving:"
      "green dots are the layer's own path, grey dots the hospital's existing feed, blue dots the model lifecycle. Press"
      <b>
        "▶ Follow one annotation"
      "to walk a norepinephrine start from the infusion pump to a signed model release, or"
      <b>
        "✦ AI"
      "to see where AI runs."
```

</details>

### `FlowOverlay`

**Role:** animated-region

Dots moving along the routed edges. Reads each edge's drawn path
       from the page, samples it with getPointAtLength, and moves dots at a
       constant speed — so the dots always ride exactly on the lines.

<details><summary>JSX outline</summary>

```
<div>
  <Diagram>
    {… .map →}
    <path>
    {… .map →}
    <g>
      <circle>
      <circle>
```

</details>

### `Key`

**Role:** panel

Line and box key for the page, plus the MVP boundary in one line.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    {… .map →}
    <div>
      <span>
      {l}
  <div>
    <b>
      "MVP (2 months):"
    "ingestion, time sync, store, annotation engine (reliability, stream correlation, intervention timestamps, first bedside-care patterns), review workbench, exports, on-prem package for one unit."
    <br>
    <b>
      "After the MVP:"
    "room sensing, voice charting, learned models trained on pilot data, MDR / HSA regulatory path, production EMR integration."
```

</details>

### `AeternisSystem` — default export

<details><summary>JSX outline</summary>

```
<Scene>
  <FlowCtx.Provider>
    <div>
      <Masthead>
      <Header>
      <StoryBar>
      <Group>
        <Hospital>
        <Partner>
      <Key>
      <FlowOverlay active={…}>
```

</details>
