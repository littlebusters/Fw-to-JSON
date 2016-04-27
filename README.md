Fireworks to JSON
=================

This command can export structure of the Fireworks PNG as a JSON file.

**I have not test on Windows.** Please send a report.

## Instllation

Download the plugin zip and unzip. And put the unziped fonlder to the Fireworks "Commands" folder.

### Commands folder location

OSX

```
"/Users/[USERNAME]/Library/Application Support/Adobe/Fireworks CS6/Commands"
```

Windows

```
C:\Users\[USERNAME]\AppData\Roaming\Adobe\Fireworks CS6\Commands
```

## Usage

1. Open the Firworks document.
1. Commands › Fw to JSON › Fw to JSON.
1. Select export folder.
1. Export completion when displayed alert.

**You have to revert the document. Because symbol is detach instance, you don't save absolutely the document.**

## Note

- This command looks for the original texture and pattern file.
- Patterned fill is exported as Fireworks PNG file.
- Bitmap export as it is.

## JSON Format

### Basic Attributes

```json
{
	"fileVersion": "1.0.0",
	"documentSetting": {
		"grid": {
			"gridSize": {
				"x": 36,
				"y": 36
			},
			"gridOrigin": {
				"x": 0,
				"y": 0
			}
		},
		"pageCount": 1,
		"docName": "document name (without extension)"
	},
	"pages": [],
	"symbols": {},
	"resExportedDir": "fw2json-exported-document name"
}
```

### "pages" Attributes

```json
"pages": [{
	"pageName": "page name",
	"backgroundColor": "#ffffff",
	"width": 500,
	"height": 500,
	"guides": {
		"x": [10, 20, 30],
		"y": [50, 60]
	},
	"frames": [{
		"topLayers": [{}]
	}]
}]
```

### "topLayers" Attributes

```json
"topLayers": [{
	"name": "layer name",
	"type": "layer",
	"locked": false,
	"visible": true,
	"parentLayerNum": -1,
	"hasChildren": true,
	"elems": [{}]
}]
```

### "elems" Attributes

#### "type = layer" Attributes

```json
"elems": [{
	"type": "layer",
	"name": "layer name",
	"visible": true,
	"locked": false,
	"parentLayerNum": -1,
	"hasChildren": true
}]
```

`parentLayerNum`: Array index of parent layer. `-1` is topLayer.

```json
"elems": [{
	"type": "rectangle",
	"name": "elems name",
	"width": 100,
	"height": 100,
	"top": 300,
	"left": 300,
	"blendMode": "normal",
	"opacity": 100,
	"visible": true,
	"locked": false,
	"pixelRect": {
		"left": 300,
		"right": 400,
		"top": 300,
		"bottom": 400
	}
}]
```

type

- rectangle
- text
- path
- group
- symbol
- slice
- layer
- bitmap
- layer

## Lisence

The MIT License (MIT)
