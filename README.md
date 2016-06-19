Fireworks to JSON
=================

This command can export structure of the Fireworks PNG as a JSON file.

**I have not test on Windows.** Please send a report.

## Instllation

Download the plugin zip and unzip. And put the unziped fonlder to the Fireworks "Commands" folder.

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

### Top Level Properties

```json
{
	"fileVersion": "1.0.0",
	"documentSetting": {},
	"pages": [],
	"symbols": {},
	"resExportedDir": "fw2json-exported-document name"
}
```

-----

### "documentSetting" Properties

```json
{
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
	}
}
```

### "pages" Properties

```json
{
	"pages": [
		{
			"pageName": "page name",
			"backgroundColor": "#ffffff",
			"width": 500,
			"height": 500,
			"guides": {
				"x": [10, 20, 30],
				"y": [50, 60]
			},
			"frames": []
		}
	]
}
```

### "symbols" Properties

```json
{
	"key_name": {
		"symbolName": "Original Symbol Name",
		"width": 75,
		"height": 75,
		"top": 31,
		"left": 387
		"elements": [],
	}
}
```

* `elements`: same `elems`

-----

### "frames" Properties

```json
{
	"frame": [
		{
			"toplayers": [{}]
		}
	]
}
```

-----

### "topLayers" Properties

```json
{
	"topLayers": [
		{
			"name": "layer name",
			"type": "layer",
			"locked": false,
			"visible": true,
			"parentLayerNum": -1,
			"hasChildren": true,
			"elems": []
		}
	]
}
```

### "elems" Properties (common properties)

- layer
- rectangle
- text
- path
- group
- symbol
- slice
- layer
- bitmap

#### "type = layer" Properties

```json
{
	"elems": [
		{
			"type": "layer",
			"name": "layer name",
			"visible": true,
			"locked": false,
			"parentLayerNum": -1,
			"hasChildren": true
		}
	]
}
```

`parentLayerNum`: Array index of parent layer. `-1` is topLayer.

#### "type = rectangle" Properties (same common properties)

```json
{
	"elems": [
		{
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
			},
			"transform": {
				"matrix": [1, 0, 0, 0, 1, 0, 0, 0, 1]
			},
			"pathAttributes": {},
			"effectList": {},
			"mask": {}
		}
	]
}
```

* `pathAttributes`: [object]
* `effectList`: [object|null]
* `mask`: [object|null]

#### "type = symbol" Properties

```json
{
	"elems": [
		{
			"type": "symbol",
			"name": "symbol instance name",
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
			"symbolID": "symbolID",
			"elements": "key_name"
		}
	]
}
```

#### "type = bitmap" Properties

```json
{
	"elems": [
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
	]
}
```

#### "type = text" Properties

```json
{
	"elems": [
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
			"transform": {
				"matrix": [1, 0, 0, 0, 1, 0, 0, 0, 1]
			},
			"pathAttributes": {},
			"effectList": {},
			"mask": {},
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
			"fontFace": "AvenirNext-Bold",
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
					"face": "AvenirNext-Bold",
					"bold": false,
					"italic": false,
					"underline": false,
					"fillColor": "#5a3f35",
					"baselineShift": 0,
					"leading": 31.9
				}
			]
		}
	]
}
```

#### "type = group" Properties

```json
{
	"elems": [
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
			"effectList": {},
			"mask": {},
			"elements": []
		}
	]
}
```

* `elements`: same `elmes` properties

#### "type = slice" Properties

```json
{
	"elems": [
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
	]
}
```

#### "type = path" Properties

```json
{
	"elems": [
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
			"effectList": {},
			"mask": {},
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
			]
		}
	]
}
```

### "pathAttributes" Properties

```json
{
	"pathAttributes": {
		"brush": {},
		"brushColor": "#3d6b3a",
		"brushPlacement": "center",
		"brushTexture": {},
		"fill": {},
		"fillColor": "#578199",
		"fillHandle1": {
			"x": 259.8141174316406,
			"y": 613.6799926757812
		},
		"fillHandle2": {
			"x": 270.8706359863281,
			"y": 613.6762084960938
		},
		"fillHandle3": {
			"x": 259.62554931640625,
			"y": 585.099609375
		},
		"fillOnTop": false,
		"fillType": "pattern"
		"fillTexture": {},
	}
}
```

* `brush`: [object|null]
* `brushColor`: [#RRGGBB|#RRGGBBAA]
* `brushTexture`: [object|null]
* `fill`: [object|null]
* `fillColor`: [#RRGGBB|#RRGGBBAA]
* `fillTexture`: [object|null]
* `fillType`: [flat|gradient|pattern|null]

#### "brush" Properties

```json
{
	"brush": {
		"alphaRemap": "none",
		"angle": 0,
		"antiAliased": false,
		"aspect": 100,
		"blackness": 38,
		"category": "bc_Charcoal",
		"concentration": 100,
		"dashOffSize1": 4,
		"dashOffSize2": 4,
		"dashOffSize3": 4,
		"dashOnSize1": 40,
		"dashOnSize2": 2,
		"dashOnSize3": 2,
		"diameter": 3,
		"feedback": "brush",
		"flowRate": 0,
		"maxCount": 14,
		"minSize": 30,
		"name": "bn_Creamy",
		"numDashes": 0,
		"sense_hdir_angle": 0,
		"sense_hdir_blackness": 0,
		"sense_hdir_hue": 0,
		"sense_hdir_lightness": 0,
		"sense_hdir_opacity": 0,
		"sense_hdir_saturation": 0,
		"sense_hdir_scatter": 0,
		"sense_hdir_size": 0,
		"sense_pressure_angle": 0,
		"sense_pressure_blackness": 60.2,
		"sense_pressure_hue": 0,
		"sense_pressure_lightness": 0,
		"sense_pressure_opacity": 50,
		"sense_pressure_saturation": 0,
		"sense_pressure_scatter": 9.4,
		"sense_pressure_size": 89.8,
		"sense_random_angle": 0,
		"sense_random_blackness": 0,
		"sense_random_hue": 0,
		"sense_random_lightness": 0,
		"sense_random_opacity": 0,
		"sense_random_saturation": 0,
		"sense_random_scatter": 6.3,
		"sense_random_size": 0,
		"sense_speed_angle": 0,
		"sense_speed_blackness": 50,
		"sense_speed_hue": 0,
		"sense_speed_lightness": 0,
		"sense_speed_opacity": 0,
		"sense_speed_saturation": 0,
		"sense_speed_scatter": 0,
		"sense_speed_size": 79.7,
		"sense_vdir_angle": 0,
		"sense_vdir_blackness": 0,
		"sense_vdir_hue": 0,
		"sense_vdir_lightness": 0,
		"sense_vdir_opacity": 0,
		"sense_vdir_saturation": 0,
		"sense_vdir_scatter": 0,
		"sense_vdir_size": 0,
		"shape": "circle",
		"softenMode": "bell curve",
		"softness": 0,
		"spacing": 31,
		"textureBlend": 36,
		"textureEdge": 96,
		"tipColoringMode": "random",
		"tipCount": 4,
		"tipSpacing": 0,
		"tipSpacingMode": "random",
		"type": "natural"
	}
}
```

#### "fill" Properties

```json
{
	"fill": {
		"category": "fc_Pattern",
		"ditherColors": [
			"#000000",
			"#000000"
		],
		"edgeType": "antialiased",
		"feather": 0,
		"gradient": {},
		"name": "pattern",
		"pattern": {},
		"shape": "pattern",
		"stampingMode": "blend opaque",
		"textureBlend": 0,
		"webDitherTransparent": false
	}
}
```

* `gradient`: [object|null]
* `pattern`: [object|null]

##### "gradient" Properties

```json
{
	"gradient": {
		"dither": false,
		"name": "cn_BlackWhite",
		"nodes": [
			{
				"color": "#ff0000",
				"isOpacityNode": false,
				"position": 0
			},
			{
				"color": "#00ff00",
				"isOpacityNode": false,
				"position": 0.5
			},
			{
				"color": "#0000ff",
				"isOpacityNode": false,
				"position": 1
			}
		],
		"opacityNodes": [
			{
				"color": "#00000023",
				"isOpacityNode": true,
				"position": 0.19697000086307526
			},
			{
				"color": "#000000",
				"isOpacityNode": true,
				"position": 0.5
			},
			{
				"color": "#00000089",
				"isOpacityNode": true,
				"position": 0.8030300140380859
			}
		],
		"gradientType": "linear"
	}
}
```

##### "pattern" Properties

```json
{
	"pattern": {
		"image": null,
		"name": "Impressionist-Blue",
		"patternURI": "file:///path/to/resource/resource-1.png",
		"filePath": false,
		"alias": "Impressionist_Blue"
	}
}
```

##### "fillTexture" Properties

```json
{
	"fillTexture": {
		"name": "Grid 4",
		"filePath": "file:///path/to/resource/Grid_4.png",
		"alias": "Grid_4"
	}
}
```

### "mask" Properties

```json
{
	"mask": {
		"mode": "mask to image",
		"element": []
	}
}
```

## Lisence

The MIT License (MIT)
