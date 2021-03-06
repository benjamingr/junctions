---
title: createConverter
---

# `createConverter(junction, [baseLocation])`

Creates a [Converter](Converter) object to help convert between [Route](Route) and [Location](Location) objects.

#### Arguments

* `junction` (*[Junction](Junction) | { [key]: [Junction](Junction) }*): The Junction or Junctions which specify the [map](/docs/introduction/locations-routes-and-maps) between Route and Location.
* `baseLocation` *<small>optional</small>* (*[Location](Location)*): Location information which must be part of every `Location` object consumed and produced by this `Converter`.

#### Returns

(*[Converter](Converter)*) A `Converter` object

#### Examples

##### Typical Usage

Pass a single [Junction](Junction), indicating that you expect [converter.route()](Converter#routelocation) to return a single `Route` for any input `Location`.

```js
// Create a Converter for a single Junction
const converter = createConverter(appJunction)
```

##### Multiple Junctions

It is also possible to pass a *group* of Junctions, indicating that multiple Routes may be active simultaneously. 

Use this feature when you want to allow one component to render multiple Routes simultaneously. For example, a modal *and* a tab bar.

```js
const converter = createConverter({

  // This Junction represents your main navigation
  main: createJunction({
    dashboard: { default: true },
    invoices: {},
    contacts: {},
  }),

  // This Junction allows you to overlay a modal over your entire application
  modal: createJunction({
    settings: {},
  }),

})
```

##### Base Location

The optional `baseLocation` argument allows you to specify parts of your `Location` objects which should be ignored by `converter.route()`, and added to locations produced by `converter.locate()`.

Use this argument if your app is being served from a subdirectory, as opposed to the root of your domain.

```js
const baseLocation = {
  pathname: '/blog/'
}
const converter = createConverter(appJunction, baseLocation)    
```
