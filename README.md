[![Build Status](https://travis-ci.org/TheProfs/drag-dropzone.svg?branch=master)](https://travis-ci.org/TheProfs/drag-dropzone)

# \<drag-dropzone\>

```bash
$ bower install --save drag-dropzone
```

## What's cool

- Includes and implements `dragDropzoneBehavior` which can be attached to
any element. You can either use the element itself, or just the behavior.
- Lightweight, has **0** dependencies
- Handles both `Files` and draggable `DOMElements`
- Handles `paste` as well

## Basic Usage

```html
<drag-dropzone></drag-dropzone>

<script>
  document.querySelector('drag-dropzone').addEventListener('item-dropped', e => {
    console.log(e.detail); // Logs items and drop position
  })
</script>
```

## Usage with DOM elements

Just make sure your DOM elements declare `type="DOMElement"` and the `data`
you want to receive when it's dropped on the drop zone.

```html
<div ondragstart="drag(event)" draggable="true">Draggable thingy</div>
<drag-dropzone></drag-dropzone>

<script>
  function drag(e) {
    e.dataTransfer.setData('type', 'DOMElement');
    e.dataTransfer.setData('data', 'foo-bar');
  }

  document.querySelector('drag-dropzone').addEventListener('item-dropped', e => {
    console.log(e.detail); // Logs items and drop position
  })
</script>
```

## Restricting file types

Set an `accepts` attribute with a comma-separated `String` of the types
it should accept.

```html
<drag-dropzone accepts="application/pdf, image/png"></drag-dropzone>

<script>
  // Assuming you dropped anything other than a PNG or PDF
  document.querySelector('drag-dropzone').addEventListener('item-error', e => {
    console.log(e.detail.text); // Logs 'Unsupported file type'
  })
</script>
```

## Using the Behavior

The element includes `dragDropzoneBehavior` which can be easily attached to
any element.

```html
<dom-module id="my-element">
  <template>
    <style>
      :host {
        display: block;
        text-align: center;
        padding: 1em;
      }
    </style>
    <label hidden$="[[!itemDragged]]">Drop Here</label>
  </template>

  <script>
    Polymer({

      is: 'my-element',

      behaviors: [
        dragDropBehavior
      ]
    });
  </script>
</dom-module>
```

## Gotchas

#### The `paste` event is attached on `window`.

If you have more than one dropzone per page, the `item-dropped` event will
be fired from all `<drag-dropzone>` elements when pasting.

In that case it makes sense to [debounce][2] the event so you handle it
only *once*.

```javascript
document.querySelector('drag-dropzone').addEventListener('item-dropped', e => {
  debounce(() => {
    // handle event
  }, 200);
})
```

There's an open [Issue][3] for the paste issues.

## Running Tests

```
$ npm install -g polymer-cli
$ polymer test
```

## Authors

- Nicholas Kyriakides, [@nicholaswmin][1], nik.kyriakides@gmail.com

## License

> Copyright (c) 2017 The Profs LTD

> Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

> The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

[1]: https://github.com/nicholaswmin
[2]: https://davidwalsh.name/javascript-debounce-function
[3]: https://github.com/TheProfs/drag-dropzone/issues/3
