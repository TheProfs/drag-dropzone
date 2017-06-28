[![Build Status](https://travis-ci.org/TheProfs/drag-dropzone.svg?branch=master)](https://travis-ci.org/TheProfs/drag-dropzone)

# \<drag-dropzone\>

## What's cool

- Minimalistic, has **0** dependencies
- Handles both `Files` and draggable `DOMElements`
- Handles `paste` as well
- Doesn't block pointer events to elements stacked below it.

## Basic Usage

```html
<drag-dropzone></drag-dropzone>

<script>
  document.querySelector('drag-dropzone').addEventListener('item-added', e => {
    console.log(e.detail);
    // logs item and dropped position
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

  document.querySelector('drag-dropzone').addEventListener('item-added', e => {
    console.log(e.detail); // includes the item
  })
</script>

```

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
