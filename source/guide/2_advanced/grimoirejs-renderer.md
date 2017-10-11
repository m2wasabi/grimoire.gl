---
type: doc
title: Renderer basics
order: 10
---

# Introduction

Rendering scene is just one of rendering strategy in Grimoire.js. You can also do many things with rendering system of Grimoire.js.

# Basics of using rendering related nodes

This GOML code is starting point of learning Grimoire.js renderer.

```xml
<goml>
    <scene>
        <camera/>
        <mesh color="red"/>
    </scene>
</goml>
```

When you inspect this code with Grimoire.js devtool, you can find there are more tags that is automatically generated. Actual goml tree structure should be like the code below.

```xml
<goml>
    <scene>
        <camera/>
        <mesh color="red"/>
    </scene>
    <renderer> <!--This tag was complemented-->
        <render-scene/>
    </renderer>
</goml>
```

This is starting point to dive rendering structure in Grimoire.js.

## \<renderer> for customizing region to be rendered

`<renderer>` node manage regions to be rendered. When this node was not generated by GOML file initially, Grimoire.js will create this node for complementing.

### Viewport of rendering region

You can customize region of viewport by using `viewport` attribute of `<renderer>`. Viewport is a term meaning a region to be rendered.

```xml
<goml>
    <scene>
        <camera/>
        <mesh color="red"/>
    </scene>
    <renderer viewport="0,0,50%,100%"/>
</goml>
```

Viewport attribute can accept comma separated values. This values are parsed as `X from left, Y from bottom, Width, Height`. **Make sure that the Y values are calculated from bottom edge**

If there were no unit at a digit, that means px. If there were % as unit, it is calculated from canvas width and height.

You can create multiple renderer in a GOML.


```xml
<goml>
    <scene>
        <camera/>
        <mesh color="red"/>
    </scene>
    <renderer viewport="0,0,50%,100%"/>
    <renderer viewport="0,50%,50%,100%"/>
</goml>
```

## Render stages for customizing what happen in rendering time

Render stages are nodes to specify how to draw viewport region. If there was no child in `<renderer>`, Grimoire create `<render-scene>` node as child of `<renderer>`.

Therefore, the previous example are complemented, and actual GOML structure should be like this.

```xml
<goml>
    <scene>
        <camera/>
        <mesh color="red"/>
    </scene>
    <renderer viewport="0,0,50%,100%">
        <render-scene/>
    </renderer>
    <renderer viewport="0,50%,50%,100%">
        <render-scene/>
    </renderer>
</goml>
```

### Using different camera in \<render-scene>

You can use multiple camera in different renderer by using `camera` attribute in `<render-scene>`.

```xml
<goml>
    <scene>
        <camera/>
        <mesh color="red"/>
    </scene>
    <renderer viewport="0,0,50%,100%"/>
    <renderer viewport="0,50%,50%,100%"/>
</goml>
```

## \<rendering-target> for offscreen rendering


## Grimoire.js renderer deep dive

