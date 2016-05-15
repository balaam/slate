# > Renderer

The renderer library is responsible for drawing things to the screen.

The render library adds two variables to the global namespace:

Key | Description
--- | -----------
`BLEND_BLEND` | The normal blend mode for sprites.
`BLEND_ADDITIVE` | Additive blend mode for sprites.


## AlignText

Sets the the alignment for any subsequent text drawn to this renderer.

```lua
gRenderer = Renderer.Create()
gRenderer:AlignText("center", "center")

function update()
    gRenderer:DrawText2d(0, 0, "Hello World")
end
```

`nil Renderer.AlignText(Renderer renderer, string alignX, string alignY)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The text alignment is set for this renderer. | ✘
alignX | string | Takes in a "left", "right" or "center" alignment value. | ✓ Default: nil
alignY | string | Takes in a "top", "bottom" or "center" alignment value. | ✓ Default: nil

## AlignTextX

Set the horizontal alignment for any subsequent text drawn to this renderer.

`nil Renderer.AlignX(Renderer renderer, string align)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The text alignment is set for this renderer. | ✘
align | string | Takes in a "left", "right" or "center" alignment value. | ✘


## AlignTextY

Set the vertical alignment for any subsequent text drawn to this renderer.

`nil Renderer.AlignY(Renderer renderer, string align)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The text alignment is set for this renderer. | ✘
align | string | Takes in a "top", "bottom" or "center" alignment value. | ✘


## Create

Create a renderer object. Usually you'll only need a single renderer. (Future work _could_, in theory, extend this to allow renderers to draw to a texture instead of the screen.)

`Renderer Renderer.Create()`

```lua
gRenderer = Renderer:Create()
gRenderer:Align("center", "center")

function update()
    gRenderer:DrawText2d(0,0,"Hello World")
end
```

## DrawCircle2d

Draw an unfilled circle to the screen. The circle is always white.

`nil Renderer.DrawCircle2d(Renderer renderer, number x, number y, number radius, number segments)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The circle is drawn using this renderer. | ✘
x | number | Center x position of circle. | ✘
y | number | Center y position of circle. | ✘
radius | number |The radius of the circle. | ✘
segments | number |The number of line segments used to draw the circle. | ✓ Default: 16

## DrawLine2d

Draw a straight 2d line segment between two points. The points can be two vectors or four numbers.

`nil Renderer.DrawLine2d(Renderer renderer, Vector start, Vector end, Vector color)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The line is drawn using this renderer. | ✘
start | Vector | Start point of the line. | ✘
end | Vector | End point ofr the line. | ✘
color | Vector | RGBA color to color the line. | ✓ Default: White

`nil Renderer.DrawLine2d(number x1, number y1, number x2, number y2, Vector color)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The line is drawn using this renderer. | ✘
x1 | Vector | x position of line start. | ✘
y1 | Vector | y position of line start. | ✘
x2 | Vector | x position of line end. | ✘
y2 | Vector | y position of line end. | ✘
color | Vector | RGBA color to color the line. | ✓ Default: White

## DrawRect2d

Draw a filled rectangle to the screen. The rectangle can be specified with two vectors or our numbers.

```lua
-- Draw a black screen over the entire render area
gRenderer:DrawRect2d(System.ScreenTopLeft(),
                     System.ScreenBottomRight(),
                     Vector.Create(0,0,0,1))
```

`nil Renderer.DrawRect2d(Renderer renderer, Vector bottomLeft, Vector topRight, Vector color)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The rectangle is drawn using this renderer. | ✘
bottomLeft| Vector | Bottom left point of rectangle. | ✘
topRight | Vector | Top right point of rectangle. | ✘
color | Vector | RGBA color to fill the rectangle with. | ✓ Default: Black

`nil Renderer.DrawRect2d(Renderer renderer, number left, number bottom, number right, number top, Vector color)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The rectangle is drawn using this renderer. | ✘
left| number | Position of left edge of the rectangle. | ✘
bottom | number | Position of the bottom edge of the rectangle. | ✘
right | number | Position of the right edge of the rectangle. | ✘
top | number | Position of the top edge of the rectangle. | ✘
color | Vector | RGBA color to fill the rectangle with. | ✓ Default: Black


## DrawSprite

Draw a sprite to the screen. Each sprite has it's own position which is where it will be drawn. Sprites are center aligned by default.

```lua
gRenderer = Renderer.Create()
gSprite = Sprite.Create()
gSprite:SetTexture(Texture.Find("logo.png"))

function update()
    gRenderer:DrawSprite(gSprite)
end
```

`nil Renderer.DrawSprite(Renderer renderer, Sprite sprite)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The sprite is drawn using this renderer. | ✘
sprite | Sprite | The sprite to draw. | ✘

## DrawText2d

Draw a string of text to the screen using the current options set for the renderer. By default text is draw aligned from the top, left.

`nil Renderer.DrawText2d(Renderer renderer, Vector pos, string text, Vector color, number width)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The text is drawn using this renderer. | ✘
position | Vector | Position to draw the text. | ✘
text | string | Text to draw. | ✘
color | Vector | Color to draw the text. | ✓ Default: White
width | number | The max width of the text before it's wrapped onto a new line | ✓ Default: -1 (no wrapping)

`nil Renderer.DrawText2d(Renderer renderer, number x, number y, string text, Vector color, number width)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The text is drawn using this renderer. | ✘
x | number | x position to render text | ✘
y | number | y position to render text | ✘
text | string | Text to draw. | ✘
color | Vector | Color to draw the text. | ✓ Default: White
width | number | The max width of the text before it's wrapped onto a new line | ✓ Default: -1 (no wrapping)

## GetKern

Kerning describes the pixel distance between two letters in a piece of text for a given font. i.e. `ll` tends to be closer together that `ww` in a non-monospace font.

A string is passed into this function because Lua doesn't have a `char` type. If the string is greater than 1 character only the first character is used.

`nil Renderer.GetKern(Renderer renderer, string char1, string char2)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The text is drawn using this renderer. | ✘
char1 | string | x position to render text | ✓ Default: '\0'
char2 | string | y position to render text | ✓ Default: '\0'

## GetRotate

Return the camera rotation in degrees for the renderer. This is 0 by default.

`number Renderer.GetRotate(Renderer renderer)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to get the rotation from. | ✘

## GetScale

Returns the scale on the X and Y axis for the current renderer. The scale is X: 1, Y: 1 by default.

`Vector Renderer.GetScale(Renderer renderer)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to get the scale from. | ✘

## GetTextRotation

Returns the current rotation applied to text drawn on the renderer, in degrees. Default rotation is 0.

`Vector Renderer.GetTextRotation(Renderer renderer)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to get the text rotation from. | ✘

## GetTranslate

Returns the X, Y translation (this can be thought of as the position or offset, if you're not familiar with the term _translation_) applied to the renderer.

`Vector Renderer.GetTranslate(Renderer renderer)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to get the translation from. | ✘

## MeasureText

Given a piece of text this will return the text's width and height for the current renderer in pixels (no rounding, so depending on the scale and font this may include fractional pixels).

`nil Renderer.MeasureText(Renderer renderer, string text, Vector output, number width)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to use when measuring the text. | ✘
text | string | The text to measure. | ✘
output | Vector | The vector to write the width and height to. These are written to the X and Y elements. | ✘
width | number | The pixel width after which the text will wrap. A value of -1 means the with is unlimited. | ✓ Default: -1

`Vector Renderer.MeasureText(Renderer renderer, string text, number width)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to use when measuring the text. | ✘
text | string | The text to measure. | ✘
width | number | The pixel width after which the text will wrap. A value of -1 means the with is unlimited. | ✓ Default: -1

## NextLine

Given a string of text, an index into that text and max width, this function returns the largest chunk of text after the index that fits within  the max width for the current render settings.

This function respects word boundaries. It won't break a word in half. i.e. "We went to the park", will never be returned as "We went to the pa", "rk", instead it would be "We went to the ", "park"

```lua
local text = "This is a lot of text and it won't fit in a small area. Therefore we might want to let the player page through it, or issue a warning etc."
gRenderer = Renderer.Create()

start, finish = gRenderer:NextLine(text, 1, 256)

print("First chunk: ", string.sub(text, start, finish))

```

`number, number Renderer.NextLine(Renderer renderer, string text, number index, number maxwidth)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to use when working out the next chunk of text that fits. | ✘
text | string | The text to break up. | ✘
index | number | Where to start in the text string. The index must be 1 or great and no greater than the text length |  ✘
width | number | The maximum width the line can be in pixels before cutting it off. |  ✘

The function returns the chunk of text that fits before the max width as two indices. The first is the start index, the second is the end.

## Rotate

Set the rotation of the renderer in degrees.

`nil Renderer.Rotate(Renderer renderer, number rotation)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to rotate. | ✘
rotation | number | The rotation to set the renderer to in degrees. | ✘

## RotateText

Set the rotation of any subsequent text commands sent to the renderer. In degrees, default is 0.

`nil Renderer.RotateText(Renderer renderer, number rotation)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to rotate. | ✘
rotation | number | The rotation for all subsequent text calls for the renderer. | ✘

## Scale

Set the scale of renderer on the X and Y axis. Default value is X: 1, Y: 1.

`nil Renderer.Scale(Renderer renderer, Vector scale)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to scale. | ✘
scale | Vector | The scale for the renderer. | ✘


`nil Renderer.Scale(Renderer renderer, number scaleX, number scaleY)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to scale. | ✘
scaleX | number | The x scale for the renderer. | ✘
scaleY | number | The y scale for the renderer. | ✓ Default: current scale on the y

## ScaleText

Set the X, Y scale for any subsequent text calls.

`nil Renderer.ScaleText(Renderer renderer, number scaleX, number scaleY)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to set the text scale for. | ✘
scaleX | number | The text x scale for the renderer. | ✘
scaleY | number | The text y scale for the renderer. | ✓ Default: 0

## ScaleTextX

Set the horizontal scale for any subsequent text calls.

`nil Renderer.ScaleTextX(Renderer renderer, number scale)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to set the text scale for. | ✘
scale | number | The text x scale for the renderer. | ✘


## ScaleTextY

Set the vertical scale for any subsequent text calls.

`nil Renderer.ScaleTextY(Renderer renderer, number scale)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to set the text scale for. | ✘
scale | number | The text y scale for the renderer. | ✘

## SetBlend

Set the blend mode for any subsequent calls to the renderer. Additive blend works well for some particle effects, laser, explosions etc.

```lua
gRenderer = Renderer.Create()
gRenderer:SetBlend(BLEND_ADDITIVE)
```
There are two blend modes:

- `BLEND_BLEND`
- `BLEND_ADDITIVE`

`nil Renderer.SetBlend(Renderer renderer, number blend)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to set the blend mode for. | ✘
blend | number | The number for the blend mode. 1 is normal, 2 is additive. There are some globals added by the renderer to make it more friendly to use. | ✘

## SetFont

Set a font to be used for any subsequent draw text calls. All fonts must be included in the manifest before they can be used.

`nil Renderer.SetFont(Renderer renderer, string fontName)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to set the font for. | ✘
fontName | string | The name of the font is defined in the manifest file. | ✘

## Translate

Set the translation for the renderer.

`nil Renderer.Translate(Renderer renderer, Vector position)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to translate. | ✘
position | Vector | New offset for the renderer. Values are taken from the X, Y elements. | ✘

`nil Renderer.Translate(Renderer renderer, number x, number y)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
renderer | Renderer | The renderer to scale. | ✘
x | number | The x scale for the renderer. | ✘
y | number | The y scale for the renderer. | ✓ Default: current y position
