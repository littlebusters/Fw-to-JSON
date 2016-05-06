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
	"frames": []
}]
```

### "frames" Attribute

```json
"frame": [
	{
		"toplayers": [{}]
	},
	{
		"toplayers": [{}]
	}
]

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

#### "type = rectangle" Attributes

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

#### "type = symbol" Attributes

```json
{
	"type": "symbol",
	"name": "symbol inctance name",
	"width": 100,
	"height": 100,
	"top": 0,
	"left": 0,
	"blendMode": "normal",
	"opacity": 100,
	"visible": true,
	"locked": false,
	"pixelRect": {
		"left": 0,
		"right": 100,
		"top": 0,
		"bottom": 100
	},
	"symbolName": "symbol name",
	"symbolID": "master579c4064",
	"elements": "master579c4064__panelSymbol__252__345"
}
```

#### "type = bitmap" Attributes

```json
{
	"type": "bitmap",
	"name": "bitmap layer name",
	"width": 100,
	"height": 100,
	"top": 0,
	"left": 0,
	"blendMode": "normal",
	"opacity": 100,
	"visible": true,
	"locked": false,
	"pixelRect": {
		"left": 0,
		"right": 100,
		"top": 0,
		"bottom": 100
	},
	"uri": "file:///path/to/resource-1.png"
}
```

#### "type = text" Attributes

```json
{
	"type": "text",
	"name": "text layer name",
	"width": 179,
	"height": 17,
	"top": 642,
	"left": 123,
	"blendMode": "normal",
	"opacity": 100,
	"visible": true,
	"locked": false,
	"pixelRect": {
		"left": 125,
		"right": 300,
		"top": 646,
		"bottom": 657
	},
	"pathAttributes": {},
	"rawHeight": 13,
	"rawWidth": 175,
	"rawTop": 644,
	"rawLeft": 125,
	"autoExpand": true,
	"antiAliasMode": "smooth",
	"antiAliased": true,
	"autoKern": true,
	"orientation": "horizontal left to right",
	"textChars": "text value",
	"transform": {
		"matrix": [1, 0, 0, 0, 1, 0, 0, 0, 1]
	},
	"fontFace": "Geometric415BT-MediumA",
	"fontSize": "11",
	"alignment": "right",
	"underline": false,
	"fillColor": "#5a3f35",
	"baselineShift": 0,
	"paragraphIndent": 0,
	"paragraphSpacingBefore": 0,
	"paragraphSpacingAfter": 0,
	"leading": 31.9,
	"textRuns": [
		{
			"characters": "text value",
			"size": "11",
			"face": "Geometric415BT-MediumA",
			"bold": false,
			"italic": false,
			"underline": false,
			"fillColor": "#5a3f35",
			"baselineShift": 0,
			"leading": 31.9
		}
	]
}
```

#### "type = group" Attributes

```json
{
	"type": "group",
	"name": "group layer name",
	"width": 100,
	"height": 100,
	"top": 0,
	"left": 0,
	"blendMode": "normal",
	"opacity": 100,
	"visible": true,
	"locked": false,
	"pixelRect": {
		"left": 0,
		"right": 100,
		"top": 0,
		"bottom": 100
	},
	"elements": [{}]
}
```

#### "type = slice" Attributes

```json
{
	"type": "slice",
	"name": "slice layer name",
	"width": 100,
	"height": 100,
	"top": 0,
	"left": 0,
	"blendMode": "normal",
	"opacity": 100,
	"visible": true,
	"locked": false,
	"pixelRect": {
		"left": 0,
		"right": 100,
		"top": 0,
		"bottom": 100
	},
	"baseName": "export name",
	"exportOptions": {
		"exportFormat": "PNG",
		"jpegQuality": 80
	}
}
```

#### "type = path" Attributes

```json
{
	"type": "path",
	"name": "path",
	"width": 1.9254150390625,
	"height": 3.3251953125,
	"top": 583.602783203125,
	"left": 342.29315185546875,
	"blendMode": "normal",
	"opacity": 100,
	"visible": true,
	"locked": false,
	"pixelRect": {
		"left": 342,
		"right": 345,
		"top": 583,
		"bottom": 587
	},
	"pathAttributes": {},
	"bezierPath": [
		{
			"isClosed": true,
			"nodes": [
				{
					"isCurvePoint": false,
					"x": 342.5592041015625,
					"y": 585.4647216796875,
					"succX": 342.5592041015625,
					"succY": 585.4647216796875,
					"predX": 342.5592041015625,
					"predY": 585.4647216796875
				},
				{
					"isCurvePoint": false,
					"x": 343.86846923828125,
					"y": 583.602783203125,
					"succX": 343.86846923828125,
					"succY": 583.602783203125,
					"predX": 343.86846923828125,
					"predY": 583.602783203125
				},
				{
					"isCurvePoint": false,
					"x": 344.21856689453125,
					"y": 583.7606811523438,
					"succX": 344.21856689453125,
					"succY": 583.7606811523438,
					"predX": 344.21856689453125,
					"predY": 583.7606811523438
				},
				{
					"isCurvePoint": false,
					"x": 342.29315185546875,
					"y": 586.927978515625,
					"succX": 342.29315185546875,
					"succY": 586.927978515625,
					"predX": 342.29315185546875,
					"predY": 586.927978515625
				}
			]
		}
	],
	"effectList": {}
}
```

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
