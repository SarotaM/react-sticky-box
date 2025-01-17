---
title: react-sticky-box Simple Example
layout: ../../layouts/MainLayout.astro
setup: |
  import {Body, Row, Content} from '../../components/ui.jsx'
  import {StickySidebar, BottomStickySidebar} from '../../components/Sidebar.jsx'
  import CodeSample from '../../components/CodeSample.astro'
---

# Simple Example

## Stick to Top

<CodeSample>

<Row slot="result">
  <StickySidebar elements={10} offsetTop={20} offsetBottom={20} client:idle />
  <Content size="lg">
    <p>Main Content.</p>
    <p>
      Go ahead and hit the <b>expand</b> button to see how it behaves once the sidebar becomes
      greater than the viewport.
    </p>
  </Content>
</Row>

```jsx
<div style={{display: "flex"}}>
  <StickyBox offsetTop={20} offsetBottom={20}>
    <Sidebar />
  </StickyBox>
  <div>Content</div>
</div>
```

</CodeSample>

## Stick to Bottom

Note the `align-items: flex-end` which forces the Sidebar to be aligned towards the bottom in addition to set `bottom={true}` on the `StickyBox` itself

<CodeSample>

<Row slot="result" alignItems="end">
  <BottomStickySidebar elements={10} offsetTop={20} offsetBottom={20} client:idle />
  <Content size="lg">
    <p>Main Content.</p>
    <p>
      Go ahead and hit the <b>expand</b> button to see how it behaves once the sidebar becomes
      greater than the viewport.
    </p>
  </Content>
</Row>

```jsx
<div style={{display: "flex", alignItems: "flex-end"}}>
  <StickyBox offsetTop={20} offsetBottom={20} bottom>
    <Sidebar />
  </StickyBox>
  <div>Content</div>
</div>
```

</CodeSample>
