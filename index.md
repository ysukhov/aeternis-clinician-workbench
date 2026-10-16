# index
*route:* `/index`

## Components

### `PageItem`

<details><summary>JSX outline</summary>

```
<button>
  <span>
    {label}
  <span>
    {formatMtime(…)}
```

</details>

### `Index` — default export

<details><summary>JSX outline</summary>

```
<div>
  <style>
    {FONTS}
  <aside>
    <header>
      <div>
        "Pages"
      <div>
        {… ? … : …}
        "Nothing drawn yet"
        <TemplateLiteral>
    <input type="search">
    <div>
      <div>
        <button title="Up one level">
          <IconArrowLeft>
        <div>
          <button>
            "Home"
          {… .map →}
          <span>
            <span>
              "/"
            <button>
              {seg}
      <nav>
        {searchResults ? … : …}
        <ConditionalExpression>
        {… && …}
        <div>
          {… ? … : …}
          "Pages the conversation draws are listed here."
          "This folder is empty."
        {… .map →}
        <button title={`…`}>
          <span>
            <span>
              <IconFolder>
            <span>
              {folder}
            <span>
              <IconChevronRight>
        {… .map →}
        <PageItem label={name} active={…}>
  <main>
    {selected ? … : …}
    <iframe title={selected}>
    <div>
      <div>
        {… ? … : …}
        "Nothing is drawn yet"
        "No page open"
      <div>
        {… ? … : …}
        "Tell the conversation what to draw. Each page it draws is listed on the left, newest first."
        "Pick a page on the left."
```

</details>
