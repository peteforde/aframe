---
title: Mixins
type: core
layout: docs
parent_section: core
order: 7
---

Mixins provide a way to compose and reuse commonly-used sets of component properties. They are defined using the `<a-mixin>` element and are placed in [`<a-assets>`][assets]. Mixins should be set with an `id`, and when an entity sets that `id` as its `mixin` attribute, the entity will absorb all of the mixin's attributes.

```html
<a-assets>
  <a-mixin id="red" material="color: red"></a-mixin>
  <a-mixin id="blue" material="color: blue"></a-mixin>
  <a-mixin id="cube" geometry="primitive: box"></a-mixin>
</a-assets>

<a-scene>
  <a-entity mixin="red cube"></a-entity>
  <a-entity mixin="blue cube"></a-entity>
</a-scene>
```

The entity with `red cube` will take the properties from the `red` mixin and the `cube` mixin in that order. Likewise with the `blue cube`. Conceptually, the entities above expand to:

```html
<a-entity material="color: red" geometry="primitive: box"></a-entity>
<a-entity material="color: blue" geometry="primitive: box"></a-entity>
```

## Overriding Component Properties

When an entity includes multiple mixins that define the same component
properties, the right-most mixin takes precedence. In the example below, the
entity includes both `red` and `blue` mixins, and since the `blue` mixin is
included last, the final color of the cube will be blue.

```html
<a-assets>
  <a-mixin id="red" material="color: red"></a-mixin>
  <a-mixin id="blue" material="color: blue"></a-mixin>
  <a-mixin id="cube" geometry="primitive: box"></a-mixin>
</a-assets>

<a-scene>
  <a-entity mixin="red blue cube"></a-entity>
</a-scene>
```

If an entity itself defines a property that is already defined by a mixin, the entity's definition takes precedence. In the example below, the entity includes both `red` and `blue` mixins and also defines a green color. Since the entity directly defines its own color, the final color of the cube will be green.

```html
<a-assets>
  <a-mixin id="red" material="color: red"></a-mixin>
  <a-mixin id="blue" material="color: blue"></a-mixin>
  <a-mixin id="cube" geometry="primitive: box"></a-mixin>
</a-assets>

<a-scene>
  <a-entity mixin="red blue cube" material="color: green"></a-entity>
</a-scene>
```

[assets]: ./assets.md
