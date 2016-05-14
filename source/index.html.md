---
title: Dinodeck Documentation

language_tabs:
  - lua

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
    - renderer
    - savegame
    - sound
    - soundstream
    - sprite
    - system
    - texture
    - time
    - touch
    - vector

search: true
---

# Introduction

Dinodeck is a multiplatform, fast, rapid game development library. Powered by Lua, using OpenGL for graphics.

You can download the latest version from the website [dinodeck.com](http://dinodeck.com).

This is documentation for version 1.0 of the engine.

# Structure

The Dinodeck engine is usually called ***dinodeck_win.exe*** on windows and ***dinodeck_mac*** on mac. When run dinodeck does the following.

1. Checks the local directory for **settings.lua**.
2. If **settings.lua** doesn't exist in the local directory, it will attempt to look inside ***data.7z*** in the loca directory and see if the file exists in that. This is true for all files it attempts to load.
3. Reads settings.lua and creates a window to display graphics and a console to display debugging information.
4. It then loads a manifest file specified in the **settings.lua** file. This is usually **manifest.lua**
5. The manifest is a list of assets; code files, fonts, textures, sounds etc. These are loaded into memory.
6. The game loop then starts. The settings.lua file specifies which file is the main file and which function to call each frame. By default this is usually ***main.lua*** and `update()`.
7. The program then runs until exited.

## settings.lua

This file controls the overall settings for the game.
It's Lua file, so it can contain Lua code.

> Here is a default settings file.

```lua
name = "The CGGameLoop"
width = 1280/2
height = 720/2
manifest = "manifest.lua"
main_script = "main.lua"
on_update = "update()"

webserver = true
```

### Settings Fields

Field | Default | Description
--------- | ------- | -----------
name | "CGGameLoop" | The name of your game. Appears on the window titlebar.
width | 640 | The width of the render area in pixels.
height | 360 | The height of the render area in pixels.
main_script | "main.lua" | This is the first file lua file execute and where the `on_update` function is expected to exist.
on_update | "update()" | The main game loop called once per frame.
manifest | "" | The manifest file is described below. It contians the list of all the files the game needs.
webserver | false | Sets up a local webserver. Used for debugging.
orientation | "portrait" | If you're tinkering with mobile then this is the default orientation to start in.

### Webserver

If the `webserver` flag is set to `true` in the **settings.lua** file then dinodeck will run a local webserver on port 8080. The webbrowser is used for debugging.

> You can connect locally to the webserver through this address.

```
http://127.0.0.1:8080/
```

The webserver doesn't serve any HTML by default, so if you try and view it using your browser nothing will happen. The webserver is a RESTful type setup.

<aside class="warning">The webserver does not work on mac. It should be run on a seperate thread and isn't ...</aside>

Reset the game with this call.

`http://127.0.0.1:8080/reset/`

Get the last error with this call.

`http://127.0.0.1:8080/lasterror/`

Run arbitary lua code with this call

`http://127.0.0.1:8080/execute/`

> Run this curl command and it will overwrite the `update` loop with one that prints "Hello" to the screen.

```shell
curl -XPOST -d 'update = function()
    gRenderer = Renderer.Create()
    gRenderer:DrawText2d(0,0, "Hello")
end' 'http://127.0.0.1:8080/execute/'
```

Data for the execute command is provided through the post data.

#### Why!?

Using these commands you can use Dinodeck almost like an interactive editor. Tell it reload from your text editor, or send over a snippet of code, interatively query the program at runtime. It's a pretty powerful idea and one that that's not been fully explored!

<aside class="warning">For a public release the <code>webserver</code> flag should be set to <code>false</code>.</aside>

### Orientation

This is a mobile only flag. If the value is any string but `"potrait"` then landscape mode will be chosen. Orientation swaps the values of System.ScreenWidth and System.ScreenHeight as well as the x and y axes.

The expected value is `"portrait"` or `"landscape"`.

## manifest.lua

The manifest file is a list of all the assets the game uses. Like the settings file it is a standard Lua file.

The manifest file is expected to have a table at the global level called "manifest". This table can then have serveral different types of child table, each representing a different catergory of asset. This is best explain by showing an example.

> An example manifest file

```lua
manifest =
{
    scripts =
    {
        ['Main.lua'] =
        {
            path = "main.lua"
        },
    },
    fonts =
    {
        ['font'] =
        {
            path = "font.ttf"
        },
    },
    textures =
    {
        ['control_bar.png'] =
        {
            path = "control_bar.png",
            scale = "pixelart"
        },
    }
}
```

All assets are represented by a key, value pair. The key is the name of the asset that can be used in the project to access it, the value is table with the path to the asset file and additional meta data about how to treat the asset.

### Supported Top Level Tables

Name |  Description
--------- | -----------
scripts | Lua scripts.
fonts | Font files.
textures | Image files.
sounds | Sound files.
soundstreams | Sound files to be streamed off disk. **Not supported**

# General Notes

## Escape To Quit

At the moment pressing Escape will close the application. This isn't a very good default behaviour and will be removed in a future update.

## Running Multiple Versions

If you run multiple versions with the webserver enabled they try to open the same ports and every version after the first application won't shut down cleanly.

# Global Functions

Dinodeck injects a few global functions into Lua namespace.

Function | Parameters | Description
--------- | ------- | -----------
`LoadLibrary` | string | Used to load libraries into the Lua namespace.
`GetDeltaTime` | n/a | Seconds since last frame.
`GetTime` | n/a | Seconds since epoch. Wraps the [c `time` function](https://en.wikipedia.org/wiki/C_date_and_time_functions).


## LoadLibrary

> Example use of `LoadLibrary`

```lua
LoadLibrary('Renderer')
```

`nil LoadLibrary( string )`

LoadLibrary takes in a string that must be the name of a valid library.

Library names are case sensitive, trying to load a library that doesn't exist will cause Dinodeck a to enter a crash state.

Name |  Description
--------- | -----------
Asset | Access assets specified in the manifest file.
Http | Send Http messages.
HttpPostData | Add POST data to http messages.
Keyboard | Check keyboard input.
Matrix | Matrix class.
Mouse | Check mouse input.
Renderer | Draw things to the screen.
SaveGame | Save and load data.
Sound | Play sounds.
SoundStream | Stream sounds from the disk. **Not supported**.
Sprite | Create and draw 2d sprites.
System | System functions.
Texture | Load textures and assign them to sprites.
Time | Time functions.
Touch | Touch input. Mobile only.
Vector | Vector class.

## GetDeltaTime

> Example use of `GetDeltaTime`

```lua
gDt = GetDeltaTime()
```

`nil GetDeltaTime( nil )`

Returns the time in seconds that the last frame took to execute.

Delta is often used to make animation run smoothly no matter the game speed. Dinodeck's frames are capped at 60 frames per second.

## GetTime

> Example use of `GetTime`

```lua
local time_now = GetTime()
```

`number GetTime( nil )`

Returns the time in seconds that have elapsed since midnight Coordinated Universal Time (UTC), 1 January 1970 (i.e. Unix Epoch time). Often used for seeding Lua's random number generator.


# Libraries

Dinodeck comes with a number of built in libraries. These can be loaded into your game using the `LoadLibrary` function.

# > Asset

Assets are files used by the game. In practice we only care about the lua files in the manifest.

## Run

> Example use of `Asset.Run`

> ***manifest.lua***

```lua
manifest =
{
    scripts =
    {
        ['Main.lua'] =
        {
            path = "main.lua"
        },
        ['AnotherFile.lua']
        {
            path = "AnotherFile.lua"
        }
    }
}
```

> ***main.lua***

```lua
Asset.Run('AnotherFile.lua')
```

`nil Asset.Run( string asset_name )`

`asset_name` is expected to be a string.

The function takes in the name of an asset as defined in the manifest file. It then executes the asset.

Assets are most commonly Lua scripts, using Asset.Run allows projects to be composed of multiple scripts.

# > Http

The Http library allows data to be retrieved and sent from websites. This opens up the possibility of leaderboards, asynchronous multiplayer game, cloud saves, integration of social services and interesting things of that sort.

## Post

> Example use of Http.Post

```lua
Http.Post("http://www.example.com",
        nil,
        function(data)
            print('Success:', data)
        end,
        function()
            print('Failure')
        end)
```

> Here data will be the html page of "http://www.example.com".

`nil Http.Post(string url, HttpPostData post_data, function OnSuccess, function OnFailure)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
url | string | The http address to contact. | ✘ |
post_data | HttpPostData | Data to attach to the http request and send to the target webpage. | ✓  Default: nil
OnSuccess | function | A lua function that gets called on successfully contacting the target site. | ✘
OnFailure | function | A lua function that gets called on failing to contact the target site | ✘


Send a POST request to a website. `OnSuccess` is called if contact is successfully made with the website. `OnFailure` occurs if the request times out or there's a failure to contact the website. The `OnSuccess` function maybe be passed the information from the website as a string. `PostData` can be sent with the request, such as a highscore, or it may be nil if no postdata is required.

## HttpPostData

Used to attach data to a Http POST request.

## Create

> Example of creating a HttpPostData object.

```lua
local postData = HttpPostData.Create("application/x-www-form-urlencoded")
```

`HttpPostData HttpPostData.Create( string content_type )`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
content_type | string | Controls how post data is attached : "multipart/form-data" or "application/x-www-form-urlencoded" | ✘

Creates a HttpPostData object. The encoding_type may be "application/x-www-form-urlencoded" or "multipart/form-data".

Generally it's best to use "multipart/form-data" but it also depends on the site you're sending the data to.

### application/x-www-form-urlencoded

The data is attached to the end of the URL

### multipart/form-data

The data is attached to the request to the request in chunks.

## AddValue

> Add Value example

```lua
local postData = HttpPostData.Create("application/x-www-form-urlencoded")
postData:AddValue("data", "{score=1000}")
```

`nil HttpPostData.AddValue(string key, string value)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
key | string | The string id of the data to attach to the request. | ✘
value | string | The string value of the data to attach to the request. | ✘

Adds a key value pair to the post data that can then be sent on to the post request.

# > Keyboard

The keyboard library lets you query the state of the keys.

The following globals are added to query the state of keys. Each entry is an integer value representing the keycode.

Key | Description
--- | -----------
`KEY_BACKSPACE` | The Backspace key.
`KEY_TAB` | The Tab key.
`KEY_CLEAR` | The 5 key on a numpad when NumLock is off.
`KEY_RETURN` | The Return / Enter key.
`KEY_PAUSE` | The Pause key.
`KEY_ESCAPE` | The Escape key.
`KEY_SPACE` | The Space key.
`KEY_EXCLAIM` | The ! key.
`KEY_QUOTEDBL` | The &quot; key.
`KEY_HASH` | The # key.
`KEY_DOLLAR` | The $ key.
`KEY_AMPERSAND` | The & key.
`KEY_QUOTE` | The ' key.
`KEY_LEFTPAREN` | The ( key.
`KEY_RIGHTPAREN` | The ) key.
`KEY_ASTERISK` | The * key.
`KEY_A` | The A key.
`KEY_B` | The B key.
`KEY_C` | The C key.
`KEY_D` | The D key.
`KEY_E` | The E key.
`KEY_F` | The F key.
`KEY_G` | The G key.
`KEY_H` | The H key.
`KEY_I` | The I key.
`KEY_J` | The J key.
`KEY_K` | The K key.
`KEY_L` | The L key.
`KEY_M` | The M key.
`KEY_N` | The N key.
`KEY_O` | The O key.
`KEY_P` | The P key.
`KEY_Q` | The Q key.
`KEY_R` | The R key.
`KEY_S` | The S key.
`KEY_T` | The T key.
`KEY_U` | The U key.
`KEY_V` | The V key.
`KEY_W` | The W key.
`KEY_X` | The X key.
`KEY_Y` | The Y key.
`KEY_Z` | The Z key.
`KEY_UP` | The up arrow key.
`KEY_DOWN` | The down arrow key.
`KEY_RIGHT` | The right arrow key.
`KEY_LEFT` | The left arrow key.
`KEY_INSERT` | The insert key.
`KEY_HOME` | The home key.
`KEY_END` | The end key.
`KEY_PAGEUP` | The page up key.
`KEY_PAGEDOWN` | The page down key.
`KEY_RSHIFT` | The right shift key.
`KEY_LSHIFT` | The left shift key.
`KEY_RCTRL` | The right control key.
`KEY_LCTRL` | The left control key.
`KEY_RALT` | The right alt key.
`KEY_LALT` | The left alt key.

<aside class="warning">The number keys are not exposed. That is certainly an oversight!</aside>

## Held

> Example of the `Held` function.

```lua
LoadLibrary(Keyboard)
LoadLibrary(Renderer)

gRenderer = Renderer:Create()
gRenderer:AlignText("center", "center")
function update()
    if Keyboard.Held(KEY_A) then
        gRenderer:DrawText2d(0, -20, "The A key is being held.")
    end
end
```

`bool Keyboard.Held( int key_code)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
key_code  | int | The key to check if held. Refer to the table in the Keyboard Library for a full lisitng of key codes. | ✘

Returns true if the key is currently being pressed.

## JustReleased

`bool Keyboard.JustReleased( int key_code )`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
key_code  | int | The key to check if held. Refer to the table in the Keyboard Library for a full lisitng of key codes. | ✘

Returns true if the key was released during the previous frame.

## JustPressed

`bool Keyboard.JustPressed( int key_code )`

Returns true if the key was pressed during the previous frame.

# > Matrix

A matrix 4x4 class. Matrices are useful for transformations.

## Create

> Example Matrix `Creates` functions.

```lua
LoadLibrary(Matrix)

local m = Matrix:Create() -- identity
local m2 = Matrix:Create(m) -- clone

local m3 = Matrix:Create(
    Vector.Create(1, 0, 0, 0),
    Vector.Create(0, 1, 0, 0),
    Vector.Create(0, 0, 1, 0),
    Vector.Create(0, 0, 0, 1),
  )
```

`Matrix Matrix.Create( nil )`

If no data is passed in then a the matrix is initialised to the identity matrix.

> The identity matrix.

```lua
1, 0, 0, 0,
0, 1, 0, 0,
0, 0, 1, 0,
0, 0, 0, 1
```

`Matrix Matrix.Create( Matrix m )`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
m  | Matrix | Data is copied from this matrix to create new one. | ✘


`Matrix Matrix.Create(
  Vector row0,
  Vector row1,
  Vector row2,
  Vector row3
)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
row0 | Vector | First row of the matrix as a vector | ✘
row1 | Vector | Second row of the matrix as a vector | ✘
row2 | Vector | Third row of the matrix as a vector | ✘
row3 | Vector | Forth row of the matrix as a vector | ✘

This function creates a new matrix object.

## Multiply

The multiply operation supports matrix, matrix multiplication and matrix vector multiplication.

`Matrix Matrix.Create(Matrix lhs, Matrix rhs)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
lhs | Matrix | Left-hand side matrix in the multiplication. | ✘
rhs | Matrix | Right-hand side matrix in the multiplication. | ✘

`Vector Matrix.Create(Matrix lhs, Vector rhs)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
lhs | Matrix | Left-hand side matrix in the multiplication. | ✘
rhs | Vector | Right-hand side vector in the multiplication. | ✘


## SetColumn

This function lets us update a column inside a matrix.

`nil Matrix.SetColumn(Matrix m, int index, Vector v)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
m | Matrix | Matrix to update. | ✘
index | number | The matrix column to update 1 - 4. | ✘
v | Vector | The values to write into the column. | ✘

`nil Matrix.SetColumn(Matrix m, int index, float x, float y, float z, float w)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
m | Matrix | Matrix to update. | ✘
index | number | The matrix column to update 1 - 4. | ✘
x | number | Value to write position 1 of the column. | ✘
y | number | Value to write position 2 of the column. | ✘
z | number | Value to write position 3 of the column. | ✘
w | number | Value to write position 4 of the column. | ✘

## SetRotation

Write a rotation transformation into the matrix.

`nil Matrix.SetRotation(Matrix m, Vector axis, float angle)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
m | Matrix | The matrix to write the rotation data to. | ✘
axis | Vector | The normal vector to rotate around. | ✘
angle | float | The amount of rotation to apply in degrees. | ✘

## SetScale

Write a scale transform into the matrix.

`nil Matrix.SetScale(Matrix m, Vector scale)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
m | Matrix | The matrix to write the scale data to. | ✘
scale | Vector | The scale to apply along the x, y and z axis. | ✘

## SetTranslate

Write a translate transform into the matrix.

`nil Matrix.SetTranslate(Matrix m, Vector translate)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
m | Matrix | The matrix to write the translate data to. | ✘
scale | Vector | The translation to apply to the x, y and z axis. | ✘

## Override: To String

Return the matrix as a string.

```lua
local m = Matrix:Create()
print(m)

> 1, 0, 0, 0,
> 0, 1, 0, 0,
> 0, 0, 1, 0,
> 0, 0, 0, 1
```

## Override: Multiple Operator

Multiply a matrix with another matrix or a vector.

```lua
local m = Matrix:Create()
local m2 = m * m            -- returns a martix
local v = Vector.Create()
local v3 = m * v            -- returns a vector
```

# > Mouse

The `Mouse` library lets us query the mouse.
The mouse adds the following global variables for querying the mouse buttons.

- `MOUSE_BUTTON_LEFT`
- `MOUSE_BUTTON_MIDDLE`
- `MOUSE_BUTTON_RIGHT`

##X

The current X position of the mouse.

`float Mouse.X()`

```lua
local x = Mouse:X()
```

##Y

The current Y position of the mouse.

`float Mouse.Y()`

```lua
local y = Mouse:Y()
```

##Position

The position X, Y position of the map returned as a vector. The z coordinate is 0.

`Vector Mouse.Position()`

##PrevPosition

The position of the mouse on the previous frame.

`Vector Mouse.PrevPosition()`

##Difference

The difference between the `PrevPosition` and the `Position` as a vector.

`Vector Mouse.Difference()`

##JustPressed

If a mouse button has just been pressed down.

`bool Mouse.JustPressed(int mouseButton)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
mouseButton | int | The mouse button to test either left, middle or right. | ✘

```lua
if Mouse.JustPressed(MOUSE_BUTTON_LEFT) then
    print("Left mouse button pressed.")
end
```

##JustReleased

If a mouse button has just been pressed released.

`bool Mouse.JustReleased(int mouseButton)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
mouseButton | int | The mouse button to test either left, middle or right. | ✘

```lua
if Mouse.JustPressed(MOUSE_BUTTON_LEFT) then
    print("Left mouse button released.")
end
```

##Held

Is the current mouse button being held.

`bool Mouse.Held(int mouseButton)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
mouseButton | int | The mouse button to test either left, middle or right. | ✘

```lua
-- This draws the hello world text next to the mouse position.
gRenderer = Renderer.Create()
if Mouse.Held(MOUSE_BUTTON_LEFT) then
    local pos = Mouse.Position()
    gRenderer:DrawText2d(pos:X(), pos:Y(), "Hello World")
end
```







