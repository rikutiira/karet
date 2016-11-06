[![npm version](https://badge.fury.io/js/karet.svg)](http://badge.fury.io/js/karet) [![Build Status](https://travis-ci.org/calmm-js/karet.svg?branch=master)](https://travis-ci.org/calmm-js/karet) [![](https://david-dm.org/calmm-js/karet.svg)](https://david-dm.org/calmm-js/karet) [![](https://david-dm.org/calmm-js/karet/dev-status.svg)](https://david-dm.org/calmm-js/karet?type=dev)

This is an experimental library that allows you to
embed [Kefir](http://rpominov.github.io/kefir/) observables
into [React](https://facebook.github.io/react/) Virtual DOM.

## Reference

To use Karet, you simply import it as `React`

```jsx
import React from "karet"
```

and you can then write React components

```jsx
const oncePerSecond = Kefir.interval(1000).toProperty(() => {})

const Clock = () =>
  <div>
    The time is {oncePerSecond.map(() => new Date().toString())}.
  </div>
```

with VDOM that can have embedded [Kefir](http://rpominov.github.io/kefir/)
observables.

### `karet-lift` attribute

Karet only lifts built-in HTML elements implicitly.  You can instruct Karet to
lift non-primitive elements by adding the `karet-lift` attribute to them:

```jsx
import * as RR from "react-router"

const Link = ({...props}) => <RR.Link karet-lift {...props}/>

// ...

<Link href="https://www.youtube.com/watch?v=Rbm6GXllBiw">
  {Kefir.sequentially(1000, [3, 2, 1, "Boom!"])}
</Link>
```
