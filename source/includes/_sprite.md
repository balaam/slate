# > Sprite

Sprites are used to draw images to the screen. They can be colored, moved, scaled and rotated. Sprites are pretty lightweight so you can have a lot and it should still be performant.

## Create

Create a new `Sprite` object.

`Sprite Sprite.Create()`

## GetColor

Get the color of the sprite. By default the color is white RGBA: (1, 1, 1, 1).

`nil Sprite.GetColor(Sprite s, Vector v)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to get the color from. | ✘
v | Vector | The sprite Color will be written into this vector. | ✘

`Vector Sprite.GetColor(Sprite s)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to get the color from. | ✘

## GetPosition

Get the position of the sprite. By default this is X: 0, Y: 0.

`nil Sprite.GetPosition(Sprite s, Vector v)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to get the Position from. | ✘
v | Vector | The sprite position will be written into the X, Y components of this vector. | ✘

`Vector Sprite.GetPosition(Sprite s)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to get the position from. | ✘

## GetRotation

Get the rotation of the sprite in degrees. By default this is 0.

`number Sprite.GetScale(Sprite s)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to get the rotation from. | ✘

## GetScale

Gets the scale for the sprite. By default this is X:1, Y:1.

`nil Sprite.GetScale(Sprite s, Vector v)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to get the scale from. | ✘
v | Vector | The sprite scale will be written into the X, Y components of this vector. | ✘

`Vector Sprite.GetScale(Sprite s)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to get the scale from. | ✘

## GetTexture

Gets the texture currently associated with the sprite. If no texture is assigned this returns `nil`.

```lua
-- Get pixel size of the sprite
-- s is a setup sprite
local t = s:GetTexture()
local width = t:GetWidth()
local height = t:GetHeight()
local scale = s:GetScale()
print(string.format("Sprite is %d x %d pixels",
    width * s:X(),
    height * s:Y()))
```

`Texture Sprite.GetTexture(Sprite s)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to get the texture from. | ✘

## SetColor

Set color of the sprite. This color uses a multiply blend. This means if the sprite was a white circle with a black border and it's color was set to red, the white parts would be red and the black would stay the same.

```lua
local s = Sprite.Create()
local t = Texture.Find("circle.png")
s:SetTexture(t)
s:SetColor(Vector.Create(1, 0, 0, 0))
```

The color is represented by a vector where the four color channels RGBA map to XYZW. (That's Red, Green, Blue, Alpha. The alpha channel controls the sprite's opacity).

`nil Sprite.SetColor(Sprite s, Vector color)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to set the color for. | ✘
color | Vector | The color of the sprite. XYZW elements map to RGBA. | ✘

## SetPosition

Set the position for a sprite. This is where it will be drawn when rendered. By default the position is X: 0, Y: 0; dead center of the screen.

```lua
-- Draw an image in top left corner of the screen
gRenderer = Renderer.Create()
local s = Sprite.Create()
local t = Texture.Find("monkey_face.png")
s:SetTexture(t)
s:SetPosition(System.ScreenTopLeft())

function update()
    gRenderer:DrawSprite(s)
end
```

`nil Sprite.SetPosition(Sprite s, Vector position)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to set the position for. | ✘
position | Vector | The position of the sprite. Only the X, Y elements are used. | ✘

`nil Sprite.SetPosition(Sprite s, number x, number y)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to set the position for. | ✘
x | number | The x position for the sprite. | ✘
y | number | The y position for the sprite. | ✓ Default: The current y value.

## SetRotation

Set the rotation for the sprite in degrees. The default rotation value is 0.

```lua
-- Draw a spinning monkey face on screen.

gRenderer = Renderer.Create()

local s = Sprite.Create()
s:SetTexture(Texture.Find("monkey_face.png"))

local t = 0
function update()
    t = t + GetDeltaTime()
    -- Will range from -180 to 180
    s:SetRotation(180*math.sin(t))
    gRenderer:DrawSprite(s)
end
```

`nil Sprite.SetRotation(Sprite s, number rotation)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to set the rotation for. | ✘
rotation | number | The rotation in degrees. | ✘

## SetScale

Set the scale for the sprite. 1 represents the sprites original scale. The default scale for a sprite is X: 1, Y: 1.

```lua
local s = Sprite.Create()
s:SetTexture(Texture.Find("logo.png"))
s:SetScale(10, 10) -- make it 10x as big

s:SetScale(1, 2) -- make it 2x as tall

-- reset using a vector
local originalScale = Vector.Create(1, 1)
s:SetScale(originalScale)

-- half size
s:SetScale(originalScale * 0.5)
```

`nil Sprite.SetScale(Sprite s, Vector scale)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to set the scale for. | ✘
scale | Vector | Vector to use to set the scale. X is the width, Y is the height. | ✘

`nil Sprite.SetScale(Sprite s, number scaleX, number scaleY)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to set the scale for. | ✘
scaleX | number | Scale for the sprite's width. | ✘
scaleY | number | Scale for the sprite's height. | ✓ Default: 0

<aside class="notice">The default behavior for scaleY is not very desirable.</aside>

## SetTexture

Assign a texture for the sprite to use when drawn.

```lua
Sprite s = Sprite.Create()
s:SetTexture(Texture.Find("logo.png"))
```

`nil Sprite.SetTexture(Sprite s, Texture t)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to set the texture for. | ✘
t | Texture | The texture to assign to the sprite. | ✘

## SetUVs

Set the texture coordinates for the sprite. If you're not already familiar with U,Vs they can be through as defining a rectangle to _cut_ out of the sprite's texture. By default we use the entire texture from the top left (0,0) to the bottom right (1, 1).

```lua
--Use only the top quarter of a texture
local s = Sprite.Create()
s:SetTexture(Texture.Find("logo.png"))
s:SetUVs(0, 0, 0.5, 0.5)
```

Using the function you can do neat things like scroll the UVs.

`nil Sprite.SetUVs(Sprite s, number u1, number v1, number u2, number v2)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
s | Sprite | The sprite to set the UVs on. | ✘
u1 | number | The leftmost coordinate for the texture. | ✘
v1 | number | The topmost coordinate for the texture. | ✘
u2 | number | The rightmost coordinate for the texture. | ✘
v2 | number | The bottommost coordinate for the texture. | ✘

## __tostring

A metatable entry for writing to a string. Outputs the type information.

```lua
local sprite = Sprite.Create()
print(sprite) -- "Sprite"
```
