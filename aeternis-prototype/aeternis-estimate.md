# Aeternis — MVP estimate, 2 months
*genre:* `design-draft` · *route:* `/aeternis-estimate`

The MVP in 8 weeks (two months) with one senior engineer for 320 hours,
  a project manager and a QA engineer at 10% each, everyone at €30/h.
  The page shows the calendar, the weekly load of each person, the cost by
  role and by phase, why one engineer is enough, and what has to be true
  for 8 weeks to hold. Every number is computed from the PEOPLE table.

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

### `Estimate`

**Role:** compute

Every number on the page — hours and cost per person, per phase and
       in total — derived from PEOPLE, PHASE_OF and the one €30/h rate.

<details><summary>JSX outline</summary>

```
<ObjectExpression>
```

</details>

### `Header`

**Role:** panel

Title and one-paragraph framing of the offer.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    "The MVP in 2 months with one senior engineer"
  <div>
    "One senior engineer full-time for 8 weeks, with a project manager and QA at 10% each, all at €30/h. Paid per phase: each phase ends in something Chandana can show to a hospital or an investor, and is a go / no-go point."
```

</details>

### `Headline`

**Role:** panel

Four headline numbers: total price, duration, team and the largest
       single payment the client commits to at once.

<details><summary>JSX outline</summary>

```
<Box id="headline">
  {cell(…)}
  {cell(…)}
  {cell(…)}
  {cell(…)}
```

</details>

### `Calendar`

**Role:** node

The 8-week calendar: phase bars with what each one ends in, then one
       row per person with hours per week, coloured by the phase they serve.

<details><summary>JSX outline</summary>

```
<Box id="calendar">
  <div>
    "Calendar and weekly load"
  <div>
    {… .map →}
    <div>
      <div>
        {d}
  {… .map →}
  <div>
    <div>
      <span>
        "Phase"
        {ph.n}
      "·"
      {ph.name}
    <div>
      {… .map →}
      <div>
      <div>
        {ph.ends}
      <div>
  <div>
  {… .map →}
  <div>
    <div>
      <div>
        {p.role}
      <div>
        {p.load}
        "·"
        {p.hours}
        "h"
    {… .map →}
    <BlockStatement>
  <div>
    "Hours per week; colour = the phase the hours are billed to. CTO oversight (Yevhenii Sukhov) on architecture and clinical-data safety is included and not billed."
```

</details>

### `RoleTable`

**Role:** panel

Cost by role: load, focus, hours, rate and line total, with the sum.

<details><summary>JSX outline</summary>

```
<Box id="roles">
  <div>
    "Team and cost by role"
  <div>
    <div>
      "Role"
    <div>
      "Load"
    <div>
      "Focus"
    <div>
      "Hours"
    <div>
      "Rate"
    <div>
      "Cost"
  {… .map →}
  <div>
    <div>
      {p.role}
    <div>
      {p.load}
    <div>
      {p.focus}
    <div>
      {p.hours}
    <div>
      "€"
      {RATE}
    <div>
      {eur(…)}
  <div>
    <div>
      "Total MVP"
    <div>
    <div>
    <div>
      {est.hours}
    <div>
    <div>
      {eur(…)}
```

</details>

### `Payments`

**Role:** panel

Pay-per-phase schedule: one card per phase with what it delivers,
       its hours and the amount, so the client commits a phase at a time.

<details><summary>JSX outline</summary>

```
<Box id="payments">
  <div>
    "Paid per phase"
  <Group>
    {… .map →}
    <div>
      <div>
        <div>
          {ph.n}
          "."
          {ph.name}
          <span>
            "· W"
            {…}
            "–W"
            {…}
        <div>
          {ph.what}
      <div>
        <div>
          {eur(…)}
        <div>
          {ph.hours}
          "h"
```

</details>

### `OneEngineer`

**Role:** panel

Why a single engineer covers the MVP, and how the one-person risk
       is handled — the question a client asks first about a team of one.

<details><summary>JSX outline</summary>

```
<Box id="one-engineer">
  <div>
    "Why one engineer is enough"
  {list(…)}
  <div>
    "And the team-of-one risk"
  {list(…)}
```

</details>

### `Conditions`

**Role:** panel

The conditions the 8-week plan depends on, and what stays out of
       the MVP. These are the first things to agree with Chandana.

<details><summary>JSX outline</summary>

```
<Group>
  <Box id="needs">
    <div>
      "What has to be true for 8 weeks to hold"
    {… .map →}
    <div>
      <span>
        {w}
      {t}
  <Box id="out">
    <div>
      "Not in the MVP"
    {… .map →}
    <div>
      "—"
      {t}
    <div>
      "Estimated separately after the MVP, funded by what it proves."
```

</details>

### `AeternisEstimate` — default export

<details><summary>JSX outline</summary>

```
<Scene>
  <div>
    <Masthead>
    <Header>
    <Headline>
    <Calendar>
    <Group>
      <RoleTable>
      <Payments>
    <Group>
      <OneEngineer>
      <div>
        <Conditions>
```

</details>
