# Aeternis — training & infrastructure
*genre:* `design-notebook` · *route:* `/aeternis-training-infra`

Where Aeternis computes and what it costs. Three places hold compute:
  the hospital (an edge box per unit and one core server, data stays
  there), the EU partner environment (training store, burst GPU training,
  model registry) and a small development cloud. Models are trained only
  on de-identified, clinician-confirmed labels and come back as signed
  releases that run in shadow mode before they go automatic. The cost
  table runs from the 8-week MVP (no GPU) to scale; a calculator turns
  units, GPU-hours and prices into a monthly bill and a rent-vs-own
  break-even. Prices are planning ranges, to be checked with providers.

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

### `Header`

**Role:** panel

Title, framing sentence and four facts a CFO asks first.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    "Compute stays small until the models start learning"
  <div>
    "The MVP runs on rules, so it needs no GPU. Hardware arrives with the pilot, inside the hospital. GPU spend starts only when learned models are trained on confirmed pilot labels — in bursts, in the EU, on de-identified data."
  <div>
    {fact(…)}
    {fact(…)}
    {fact(…)}
    {fact(…)}
```

</details>

### `Unit`

**Role:** node

One compute component: name, what runs on it, and its sizing line.

<details><summary>JSX outline</summary>

```
<Box id={id}>
  <div>
    <div>
      {title}
    {tag && …}
    <span>
      {tag}
  <div>
    {sub}
  {spec && …}
  <div>
    {spec}
```

</details>

### `Zone`

**Role:** layout

A titled zone for one place where compute lives.

<details><summary>JSX outline</summary>

```
<Box id={id}>
  <div>
    {title}
  <div>
    {note}
  <Group>
    {children}
```

</details>

### `SectionHead`

**Role:** panel

Numbered section heading with a one-line lead.

<details><summary>JSX outline</summary>

```
<div>
  <span>
    {title}
  <span>
    {lead}
```

</details>

### `Topology`

**Role:** layout

Where compute lives: hospital, EU partner environment and dev cloud,
       with the only data paths allowed between them.

<details><summary>JSX outline</summary>

```
<div>
  <Zone id="z-dev" title="Development cloud · EU">
    <Unit id="u-ci" title="CI & staging">
    <Unit id="u-replay" title="Replay & evaluation">
  <Zone id="z-hosp" title="Hospital · on-prem">
    <Unit id="u-edge" title="Edge box · per unit">
    <Unit id="u-core" title="Core server">
    <Unit id="u-infer" title="Model inference">
  <Zone id="z-eu" title="Partner environment · EU">
    <Unit id="u-store" title="AI training store">
    <Unit id="u-gpu" title="GPU training & evaluation">
    <Unit id="u-reg" title="Model registry">
```

</details>

### `Pipeline`

**Role:** layout

The training pipeline from a confirmed label to an automatic
       release; each step names where it runs and the gate it must pass.

<details><summary>JSX outline</summary>

```
<div>
  {… .map →}
  <Box id={s.id}>
    <div>
      <span>
        {s.n}
      <span>
        {s.where}
    <div>
      {s.title}
    <div>
      {s.text}
    <div>
      "gate ·"
      {s.gate}
```

</details>

### `CostTable`

**Role:** panel

Cost by stage, from the 8-week MVP to scale, with who pays.

<details><summary>JSX outline</summary>

```
<Box id="costs">
  <div>
    <div>
    {… .map →}
    <div>
      {s}
  {… .map →}
  <div>
    <div>
      {k}
    {… .map →}
    <div>
      {x}
  <div>
    <div>
      "Typical total"
    <div>
      "€100–200"
    <div>
      "€0.3–3k + €50–110 / mo"
    <div>
      "€100–400 / mo"
    <div>
      "€0.3–3k + €10–30 / mo per unit"
```

</details>

### `Bill`

**Role:** compute

Monthly bill, one-off hardware and the rent-vs-own curves for the
       calculator, from units, GPU-hours, rent price and server price.

<details><summary>JSX outline</summary>

```
<ObjectExpression>
```

</details>

### `BreakEvenChart`

**Role:** node

Cumulative GPU cost over 18 months: renting by the hour vs owning
       one server; the crossing month is marked when there is one.

<details><summary>JSX outline</summary>

```
<Diagram id="breakeven">
  {… .map →}
  <g>
    <line>
    <text>
      "€"
      {…}
      "k"
  {… .map →}
  <text>
    {… ? … : …}
    "now"
    <TemplateLiteral>
  <polyline>
  <polyline>
  <text>
    "rent by the hour"
  <text>
    "own one workstation"
  {… && …}
  <g>
    <line>
    <circle>
    <text>
      "break-even ≈"
      {be.toFixed(…)}
      "mo"
```

</details>

### `Calculator`

**Role:** panel

The calculator: four sliders (units, GPU-hours, rent price, server
       price) driving the monthly bill, hardware, and the break-even chart,
       with the rent-or-own recommendation in words.

<details><summary>JSX outline</summary>

```
<Box id="calc">
  <div>
    <Slider id="s-units" label="units in the pilot">
    <Slider id="s-hours" label="GPU-hours per month (training phase)">
    <Slider id="s-rate" label="GPU rent price">
    <Slider id="s-own" label="owned GPU workstation">
    <div>
      "Fixed: cloud dev"
      {eur(…)}
      "/mo · storage"
      {eur(…)}
      "/mo per unit · core server"
      {eur(…)}
      "· edge box"
      {eur(…)}
      "per unit · owned workstation power"
      {eur(…)}
      "/mo."
  <div>
    <div>
      {stat(…)}
      {stat(…)}
      {stat(…)}
    <div>
      <BreakEvenChart>
      <div>
        <div>
          "Recommendation"
        <div>
          {advice}
        <div>
          "Rule of thumb: rent unless a workstation pays back within a year — at these prices that is above ~"
          {threshold}
          "GPU-hours a month, every month."
```

</details>

### `Levers`

**Role:** panel

The five levers that keep compute cheap, each with its effect.

<details><summary>JSX outline</summary>

```
<div>
  {… .map →}
  <div>
    <div>
      {String(…).padStart(…)}
    <div>
      {k}
    <div>
      {v}
```

</details>

### `AeternisTrainingInfra` — default export

<details><summary>JSX outline</summary>

```
<Scene>
  <div>
    <Masthead>
    <Header>
    <SectionHead title="Where compute lives">
    <Topology>
    <SectionHead title="From a confirmed label to a release">
    <Pipeline>
    <SectionHead title="What it costs, stage by stage">
    <CostTable>
    <SectionHead title="Rent or own the GPU?">
    <Calculator>
    <SectionHead title="How we keep it cheap">
    <Levers>
```

</details>
