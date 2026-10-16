# Thought-to-command headset — how it would work
*genre:* `design-draft` · *route:* `/neuro-command`

Chandana's second idea: a headset that reads what a person wants to do
  and turns it into a command ("write a reply"). A non-invasive headset
  cannot read free sentences from the brain today — that has only been
  shown with implanted electrodes. What it can read reliably is a small
  set of trained intents, a selection, and a confirm. The page draws the
  product built on that: the brain gives the intent, AI writes the words,
  a deliberate signal confirms. A live demo walks one message through the
  four steps; a pipeline shows the parts; a ladder shows what each kind
  of brain signal can carry; the MVP shape and the open questions close it.

## Components

### `Masthead`

**Role:** panel

Page masthead: working title, whose idea, status — and loads the
       typefaces shared with the Aeternis pages.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    "∿"
  <div>
    <div>
      "Thought-to-command headset"
    <div>
      "Working title · idea from Dr. C. Samaranayake, outside healthcare"
  <div>
  <div>
    <span>
      "Document"
    <span>
      "NEURO-01"
    <span>
      "Revision"
    <span>
      "A, 15 Oct 2026"
    <span>
      "Status"
    <span>
      "First sketch for discussion"
```

</details>

### `Header`

**Role:** panel

Title and the one honest sentence the whole design rests on.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    "The brain gives the intent, AI writes the words"
  <div>
    "A headset worn like headphones cannot read a sentence you think — today that only works with electrodes implanted in the brain. It can reliably read a few trained intents, a choice between options, and a deliberate confirm. So the product is built on those three: think “reply”, pick what to say, confirm — and an AI writes and sends it."
```

</details>

### `EegTraces`

**Role:** animated-region

Eight EEG channels scrolling in real time. The current demo step
       shapes them: a rhythm change over C3/C4 for the trained intent, a
       steady flicker response over O1 for the choice, two sharp bursts on
       every channel for the jaw-clench confirm.

<details><summary>JSX outline</summary>

```
<Diagram id="eeg">
  {… .map →}
  <BlockStatement>
```

</details>

### `PhoneScreen`

**Role:** panel

The phone-side screen of the demo: what the decoder heard, the
       chat, the three AI drafts (one selected by gaze), and the send state.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    <span>
      "Messages · Anna"
    <span>
      "19:42"
  <div>
    "Are you coming at 7?"
  <div>
    <div>
      "Decoder"
    <div>
      {… ? … : …}
      "Reply · confidence 0.87"
      "Listening for intent…"
  {… && …}
  <CallExpression>
  {… && …}
  <div>
    "Clench twice to send"
  {… && …}
  <div>
    "Running 15 min late, start without me"
    <div>
      "sent by headset ✓"
```

</details>

### `Demo`

**Role:** animated-region

The live demo block: step bar, EEG traces, the phone screen and the
       caption saying which brain signal carries the current step.

<details><summary>JSX outline</summary>

```
<Box id="demo">
  <div>
    <button type="button">
      {playing ? … : …}
      "❚❚  Pause"
      "▶  Play"
    <div>
      {… .map →}
      <button type="button">
        {…}
        "."
        {s.title}
  <div>
    <div>
      <div>
        <span>
          "Headset · 8 dry electrodes · 250 Hz"
        <span>
          {cur.brain}
      <EegTraces>
    <PhoneScreen>
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
        "Signal used:"
        <span>
          {cur.brain}
  <div>
    "Simulated signals for illustration; not recorded data."
```

</details>

### `SignalChain`

**Role:** layout

The signal chain from scalp to decision, six steps left to right.

<details><summary>JSX outline</summary>

```
<div>
  {… .map →}
  <Box id={id}>
    <div>
      <span>
        {…}
      <span>
        {t}
    <div>
      {d}
    <div>
      {spec}
```

</details>

### `Signature`

**Role:** node

One signature chart: what the decoder actually looks for in the
       cleaned signal for one kind of command, drawn as a small plot.

<details><summary>JSX outline</summary>

```
<Box id={id}>
  <div>
    <span>
      {title}
    <span>
      {where}
  <div>
    <Diagram>
      {body}
  <div>
    {text}
```

</details>

### `Signatures`

**Role:** panel

The three signatures side by side — what the decoder looks for to
       detect an intent, a choice and a confirm.

<details><summary>JSX outline</summary>

```
<div>
  <Signature id="sig-mi" title="Intent: imagined movement">
  <Signature id="sig-ssvep" title="Choice: looking at a flicker">
  <Signature id="sig-emg" title="Confirm: two jaw clenches">
```

</details>

### `Part`

**Role:** node

One part of the system: what it is, what runs there, and an example.

<details><summary>JSX outline</summary>

```
<Box id={id}>
  <div>
    {where}
  <div>
    {title}
  <div>
    {sub}
  {eg && …}
  <div>
    {eg}
```

</details>

### `Pipeline`

**Role:** layout

The system left to right: headset, phone app, intent decoder,
       confirm gate, AI action layer, the user's apps; plus the
       per-person calibration loop under it.

<details><summary>JSX outline</summary>

```
<div>
  <div>
    <Part id="p-head" title="Headset">
    <Part id="p-app" title="Signal app">
    <Part id="p-dec" title="Intent decoder">
    <Part id="p-gate" title="Confirm gate">
    <Part id="p-ai" title="AI action layer">
    <Part id="p-apps" title="Apps">
  <div>
    <Part id="p-cal" title="Calibration & learning">
```

</details>

### `Ladder`

**Role:** panel

The ladder of what a non-invasive headset can carry, from reliable
       to not possible, each with how it is done and its status.

<details><summary>JSX outline</summary>

```
<Box id="ladder">
  <div>
    <span>
      "What the person wants to convey"
    <span>
      "How the headset picks it up"
    <span>
      "Status today"
  {… .map →}
  <div>
    <span>
      {what}
    <span>
      {how}
    <span>
      <span>
      {status}
```

</details>

### `NextSteps`

**Role:** panel

The smallest thing worth building first, and the questions that
       decide everything else; both for the next call with Chandana.

<details><summary>JSX outline</summary>

```
<div>
  <Box id="mvp">
    <div>
      "A first version worth building"
    <div>
      "Proves the loop end to end on real people, without building hardware."
    {… .map →}
    <div>
      <span>
        "✓"
      {m}
  <Box id="questions">
    <div>
      "Questions for Chandana"
    {… .map →}
    <div>
      <div>
        {q}
      <div>
        {a}
```

</details>

### `Heading`

**Role:** panel

Section heading with a one-line lead.

<details><summary>JSX outline</summary>

```
<div>
  <span>
    {title}
  <span>
    {lead}
```

</details>

### `NeuroCommand` — default export

<details><summary>JSX outline</summary>

```
<Scene>
  <div>
    <Masthead>
    <Header>
    <Demo>
    <Heading title="How the signal is read">
    <SignalChain>
    <Signatures>
    <Heading title="How it is built">
    <Pipeline>
    <Heading title="What a headset can read">
    <Ladder>
    <NextSteps>
```

</details>
