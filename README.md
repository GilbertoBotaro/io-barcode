# io-barcode

**io-barcode** is a simple way to create different types of 1d barcodes.

This started as a fork of the [Johan Lindell's JsBarcode][1] project that adds the following functionality:

1. Isomorphic barcode generation on client and server.
2. Node support through `node-canvas`.
3. Packaged with UMD support on client side.
4. Modular design
5. Returns a canvas element.
6. Removed direct jQuery integration

## Demo and examples
[Barcode Generator](http://lindell.github.io/JsBarcode/)

#### Supported barcodes
*  CODE128 (B or C)
*  EAN (13)
*  UPC-A
*  CODE39
*  ITF (Interleaved 2 of 5)
*  ITF14
*  Pharmacode

## Installation

With npm:

```
npm install io-barcode
```

Or download the [minified UMD bundle](build/browser/io-barcode.min.js).

## Usage

#### ioBarcode.TYPE(code, opts)
Create a new barcode.  Returns a canvas element.

 * `TYPE` - the type of barcode, can be:
	*  CODE128B
	*  CODE128C
	*  EAN
	*  UPC
	*  CODE39
	*  ITF
	*  ITF14
	*  Pharmacode
 * `code` - the string to encode
 * `opts` - additional formatting, default options are:
	```js
	{
		width:	2,
		height:	100,
		quite: 10,
		displayValue: false,
		font: 'monospace',
		textAlign: 'center',
		fontSize: 12,
		backgroundColor: '',
		lineColor: "#000"
	}
	```

Example on server side:

```js
  var fs = require('fs')
  var ioBarcode = require("io-barcode")
  var canvas = ioBarcode.CODE128B('Javascript is fun!', {
    width: 1,
    height: 25
  })
  var stream = canvas.pngStream()
  stream.pipe(fs.createWriteStream('./barcode.png'))
```

Example on the client side:

```js
  // If using a require system like browserify or webpack just require it
  var ioBarcode = require("io-barcode")
  // If direct via a <script> tag ioBarcode is exposed as a global
  var canvas = ioBarcode.CODE128B('Javascript is fun!', {
    width: 1,
    height: 25
  })

  // Render the canvas directly
  document.body.appendChild(canvas)

  // Or in an image tag
  var img = new Image()
  img.src = canvas.toDataURL('image/png')
  document.body.appendChild(img)
```

[1]: https://github.com/lindell/JsBarcode