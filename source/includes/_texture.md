
# > Texture

A class that represents a reference to a texture defined in the manifest file.

## Find

This is a "static" function that let's you create textures from the manifest. They're all just a reference so creating two different textures using the same file doesn't cause any siginificant overhead.

```lua
-- Imagine your manifest looks like this
manifest =
{
    scripts =
    {
        ['Main.lua'] = { path = "main.lua" },
    },
    textures =
    {
        ['logo.png'] = { path = "logo.png", },
    }
}
-- Then you load that texture in main.lua as so

local t = Texture.Find("logo.png")
string.format("The texture is %s pixels wide.",
              t:GetWidth())
-- Prints:
-- The texture is 128 pixels wide.
```

`Texture Texture.Find(string id)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
id | string | The id of the texture, as definied in the manifest file. | ✘

## GetHeight

Get the height of texture in pixels.

`number Texture.GetHeight(Texture t)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
t | Texture | The texture to get the height from. | ✘

## GetWidth

Get the width of texture in pixels.

`number Texture.GetWidth(Texture t)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
t | Texture | The texture to get the width from. | ✘

## __tostring

A metatable entry for writing to a string. Outputs the texture dimensions and type information.

```lua
local logo = Texture.Find("logo.png")
print(logo) -- "Texture [128 x 128]"
```