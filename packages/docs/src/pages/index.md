---
title: react-sticky-box documentation
layout: ../layouts/MainLayout.astro
setup: |
  import {Body, Row, Content} from '../components/ui.jsx'
  import {StickySidebar, StickyWord} from '../components/Sidebar.jsx'
  import CodeSample from '../components/CodeSample.astro'
---

# React Sticky Box

## See it in Action

<Body big>
	<Row>
		<Content size="xs" />
	</Row>
	<Row>
		<StickySidebar offsetTop={20} offsetBottom={20} elements={20} client:idle />
		<Content size="lg">
			<p>The sidebar to the left stays in a sticky position.</p>
			<p>
				Go ahead and hit the <b>expand</b> button to see how it behaves once the sidebar becomes
				greater than the viewport.
			</p>
		</Content>
	</Row>
	<Row>
		<Content size="md" />
	</Row>
</Body>

## What the Code looks like

```jsx
import React from "react";
import StickyBox from "react-sticky-box";

const Page = () => (
  <div className="row">
    <StickyBox offsetTop={20} offsetBottom={20}>
      <div>Sidebar</div>
    </StickyBox>
    <div>Content</div>
  </div>
);
```

## How to install

```bash
yarn add react-sticky-box
```

```bash
npm install react-sticky-box
```

## How it works

React Sticky Box relies on `position: sticky`. It's [widely supported](https://caniuse.com/#feat=css-sticky) these days.

For all browsers without sticky support, it falls back to a `position: relative` behaviour. This could be considered "good enough" in a lot of cases. Alternatively you have to provide a custom solution to get sticky behaviour here. Either via polyfills or even targeting IE10+ Browsers via `@media queries` like presented [here](https://github.com/codecks-io/react-sticky-box/issues/30#issuecomment-450153041) by [Olivr3](https://github.com/Olivr3).

`position: sticky` isn't without it's issues though. If the content is bigger than the viewport, it simply gets cut off and becomes inaccessible. This library solves this issue by allowing the content to scroll along with all the other content until the the corresponding end is visible and continues to be sticky.

You still might encounter browser bugs with `position: sticky` if your content lies within certain combinations of `z-index`, `overflow` and especially `transform`.

## What kind of scroll containers can be used

### Window

```jsx
<body>
  <div style={{display: "flex", alignItems: "flex-start"}}>
    <StickyBox>Sidebar</StickyBox>
    <div>Main Content</div>
  </div>
</body>
```

### Scroll Container as offset parent

```jsx
<div style={{height: 200, position: "relative", overflow: "auto"}}>
  <div style={{position: "absolute", top: 0, left: 0, right: 0, minHeight: "100%"}}>
    <div style={{display: "flex", alignItems: "flex-start"}}>
      <StickyBox>Sidebar</StickyBox>
      <div>Main Content</div>
    </div>
  </div>
</div>
```

### Scroll Container as non-offset parent

```jsx
<div style={{height: 200, overflow: "auto"}}>
  <div style={{display: "flex", alignItems: "flex-start"}}>
    <StickyBox>Sidebar</StickyBox>
    <div>Main Content</div>
  </div>
</div>
```

## Troubleshooting

### The StickyBox is not sticky!

Make sure that the `<StickyBox>` is only as high as its content, and not as high as the parent node. To quickly check this you can do:

```jsx
<StickyBox style={{border: "3px solid green"}}>content</StickyBox>
```

#### Good

<CodeSample size="sm">

<div style="display: flex; align-items: flex-start; padding: 1.5rem 2rem" slot="result">
  <StickyWord style={{border: "3px solid green"}} word="Sidebar" client:idle/>
  <div style="height: 150px; border: 3px solid blue;">Main Content</div>
</div>

```jsx
<div style={{display: "flex", alignItems: "flex-start"}}>
  <StickyBox style={{border: "3px solid green"}}>Sidebar</StickyBox>
  <div style={{height: 150, border: "3px solid blue"}}>Main Content</div>
</div>
```

</CodeSample>

#### Bad

This time without `alignItems: "flex-start"`

<CodeSample size="sm">

<div style="display: flex;padding: 1.5rem 2rem" slot="result">
  <StickyWord style={{border: "3px solid green"}} word="Sidebar" client:idle/>
  <div style="height: 150px; border: 3px solid blue;">Main Content</div>
</div>

```jsx
<div style={{display: "flex"}}>
  <StickyBox style={{border: "3px solid green"}}>Sidebar</StickyBox>
  <div style={{height: 150, border: "3px solid blue"}}>Main Content</div>
</div>
```

</CodeSample>

## Is this production-ready?

This library is heavily used within [Codecks](https://www.codecks.io), so expect it to be fairly stable.
