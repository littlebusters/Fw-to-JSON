Fireworks to JSON
=================

![JSON to Layers HERO](http://creative-tweet.net/img/github/fw-to-json-hero.png)

このコマンドは、Fireworks PNGの構造（fw.DocumentDOM()）をJSONファイルとして書き出す拡張機能です。

**Windows版のFireworksではテストをしていません。** 使われたかたは、ぜひレポートを送ってください :)

動画はこちら: [Fireworks to Sketch 3 — QuickCast.](http://quick.as/pk7yuzz8b)

動画では、このコマンドで書き出したJSONを、Sketch 3のレイヤーに変換する[JSON to Layers](https://github.com/littlebusters/JSON-to-Layers)というプラグインを使っています。

## インストール

ZIPファイルをダウンロードし伸張してください。**フォルダ名を「Fw-to-JSON-master」から「Fw to JSON」へ変更**し、FireworksのCommandsフォルダへ入れてください。

## 使い方

1. Fireworks PNGを開きます。
1. コマンド › Fw to JSON › Fw to JSONを選択します。
1. 書き出しするフォルアダを選択します。
1. アラートが表示されたら書き出しが完了です。

## 注意点

- シンボルインスタンスは内容を解析するため、シンボルからリンクを解除しています。コマンド実行後は「復帰」させるか、**必ず保存せず**閉じてください。
- ビットマップやテクスチャー・パターンは別ファイルとして書き出しを行います。非表示にしていても書き出すようにしているため、オブジェクトが多い場合はファイルを整理してから実行してください。
- 書き出しとしていますが、正確には「オブジェクトをコピー→新規ドキュメント作成→ペースト→保存」を繰り返します。結構な負荷がかかると思われますので、必ず保存をしてから実行するようにしてください。
- ビットマップは現在の状態そのままを書き出します。解像度が大きな画像でも縮小していれば、縮小した状態を100%として書き出します。
- 任意に適用しているパターンとテクスチャは、初回に読み込んだ場所を見に行きます。ファイルがない場合は、falseを設定します。改めて同じものを同じ場所に置いておくのも手です。
- "Fireworks Console" または "DOM Inspector"（もしくは両方）をインストールしている場合は、インスペクタを非表示にした状態でFireworksを再起動するか、Extension Managerで無効化してください。

## 書き出されるJSONについて

### 最上位のプロパティ

```json
{
	"fileVersion": "1.0.0",
	"documentSetting": {},
	"pages": [],
	"symbols": {},
	"resExportedDir": "fw2json-exported-document name"
}
```

### "documentSetting" プロパティ

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

### "pages" プロパティ

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

### "symbols" プロパティ

* `elements`: same `elems`

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

### "frames" プロパティ

```json
{
	"frame": [
		{
			"toplayers": [{}]
		}
	]
}
```

### "topLayers" プロパティ

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

### "elems" プロパティ (共通プロパティ)

- layer
- rectangle
- text
- path
- group
- symbol
- slice
- layer
- bitmap

#### "type = layer" プロパティ

`parentLayerNum`: Array index of parent layer. `-1` is topLayer.

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

#### "type = rectangle" プロパティ (同様の共通プロパティ)

* `pathAttributes`: [object]
* `effectList`: [object|null]
* `mask`: [object|null]

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

#### "type = symbol" プロパティ

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

#### "type = bitmap" プロパティ

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

#### "type = text" プロパティ

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

#### "type = group" プロパティ

* `elements`: same `elmes` properties

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

#### "type = slice" プロパティ

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

#### "type = path" プロパティ

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

### "pathAttributes" プロパティ

* `brush`: [object|null]
* `brushColor`: [#RRGGBB|#RRGGBBAA]
* `brushTexture`: [object|null]
* `fill`: [object|null]
* `fillColor`: [#RRGGBB|#RRGGBBAA]
* `fillTexture`: [object|null]
* `fillType`: [flat|gradient|pattern|null]

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

#### "brush" プロパティ

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

#### "fill" プロパティ

* `gradient`: [object|null]
* `pattern`: [object|null]

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

##### "gradient" プロパティ

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

##### "pattern" プロパティ

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

##### "fillTexture" プロパティ

```json
{
	"fillTexture": {
		"name": "Grid 4",
		"filePath": "file:///path/to/resource/Grid_4.png",
		"alias": "Grid_4"
	}
}
```

### "mask" プロパティ

```json
{
	"mask": {
		"mode": "mask to image",
		"element": []
	}
}
```

## バグ報告

GitHubのIssuesへお使いのOSとFireworksのバージョンを書き込んでください。

## ライセンス

MITライセンスです。詳しくは、LICENSEをご確認ください。
