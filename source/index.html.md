---
title: Dinodeck Documentation

language_tabs:
  - lua

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
    - keyboard
    - matrix
    - mouse
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

Dinodeck is a multiplatform, fast, rapid game development library. It's powered by Lua and uses OpenGL for graphics.

Dinodeck is inspired by many great engines and graphics APIs I've used in the past but with an emphasis on speed of development and ease of distribution.

You can download the latest version from the website [dinodeck.com](http://dinodeck.com).

This is documentation for [version 1.1.2](https://github.com/dinodeck/dinodeck/tree/v1.1.2) of the engine.

# Structure

The Dinodeck engine is usually called ***dinodeck_win.exe*** on windows and ***dinodeck_mac*** on mac. When executed dinodeck does the following:

1. Checks the local directory for **settings.lua**.
2. If **settings.lua** doesn't exist in the local directory, it attempts to look inside ***data.7z*** to check if the file exists there. This is true for all files it attempts to load.
3. Reads settings.lua and creates a window to display graphics and a console to display debugging information.
4. Loads a manifest file specified in the **settings.lua** file. This is usually **manifest.lua**
5. The manifest is a list of assets: code files, fonts, textures, sounds etc. These are loaded into memory.
6. The game loop then starts. The settings.lua file specifies which file is the main file and which function to call each frame. By default this is usually ***main.lua*** and `update()`.
7. The program then runs until exited.

## settings.lua

This file controls the overall settings for the game.
It's a Lua file and so can contain any Lua code.

> Here is an example settings file:

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
main_script | "main.lua" | This is the first file lua executes and where the `on_update` function is expected to exist.
on_update | "update()" | The main game loop called once per frame.
manifest | "" | The manifest file is described below. It lists all the files the game needs.
webserver | false | Sets up a local webserver. Used for debugging.
orientation | "portrait" | If you're tinkering with mobile then this is the default orientation to start in.

### Webserver

If the `webserver` flag is set to `true` in the **settings.lua** file then dinodeck runs a local webserver on port 8080. The webbrowser is used for debugging.

> You can connect locally to the webserver through this address.

```
http://127.0.0.1:8080/
```

The webserver doesn't serve any HTML by default, so if you try and view it using your browser nothing will happen. The webserver is a [RESTful](https://en.wikipedia.org/wiki/Representational_state_transfer) type setup.

Reset the game with this call.

`http://127.0.0.1:8080/reset/`

Get the last error with this call.

`http://127.0.0.1:8080/lasterror/`

Run arbitary lua code with this call

`http://127.0.0.1:8080/execute/`

> Run this curl command to overwrite the `update` loop with one that prints "Hello" to the screen.

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

This is a mobile only flag. If the value is any string but `"potrait"` then landscape mode is chosen. Orientation swaps the values of System.ScreenWidth and System.ScreenHeight as well as the x and y axes.

The expected value is `"portrait"` or `"landscape"`.

## manifest.lua

The manifest file lists the assets the game uses. Like the settings file it is a standard Lua file.

The manifest file is expected to have a table at the global level called "manifest". This table may have serveral different subtables, each representing a different category of asset. This is best explained with an example.

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

All assets are represented by a key, value pair. The key is the name of the asset (used in the project to access it), the value is table with the path to the asset file and additional meta data about how to treat the asset.

### Supported Top Level Tables

Name |  Description
--------- | -----------
scripts | Lua scripts.
fonts | Font files.
textures | Image files.
sounds | Sound files.
soundstreams | Sound files to be streamed off disk. **Not supported**

### Script Formats

Any plain text file is fine. By convention it's normal for script files to have a '.lua' extension.

### Font Formats

The font loader expects true type fonts i.e. .tff.

### Texture Formats

The following texture formats are supported:

- **BMP** - non-1bpp, non-RLE (from stb_image documentation)
- **PNG** - non-interlaced (from stb_image documentation)
- **JPG** - JPEG baseline (from stb_image documentation)
- **TGA** - greyscale or RGB or RGBA or indexed, uncompressed or RLE
- **DDS** - DXT1/2/3/4/5, uncompressed, cubemaps (can't read 3D DDS files)
- **PSD** - (from stb_image documentation)
- **HDR** - converted to LDR, unless loaded with *HDR* functions (RGBE or RGBdivA or RGBdivA2)

Dinodeck uses [SOIL](http://www.lonesock.net/soil.html) to load images. Format documentation taken from the site.

A texture asset may have an optional `scale` flag. This determines how the scaling works. By default scaling a sprite causes the texture to be interpolated; smoothing out the pixels. The `"pixelart"` flag scales using "nearest neighbor" so the pixel boundaries remain distinct.

### Sound Formats

Only .wav is supported.

# General Notes

## Running Multiple Versions

If you run multiple versions with the webserver enabled, they try to open the same port and every version after the first application will fail to shut down cleanly.

# Global Functions

Dinodeck injects a few global functions into the Lua namespace.

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

`LoadLibrary` takes in a string that must be the name of a valid library.

Library names are case sensitive, trying to load a library that doesn't exist causes Dinodeck to enter a crash state.

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

Delta is often used to make animations run smoothly no matter the game speed. Dinodeck's frames are capped at 60 frames per second.

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

`nil Asset.Run( string assetName )`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
assetName | string | Name of an asset defined in the manifest file. | ✘

The function takes in the name of an asset as defined in the manifest file. It then executes the asset.

Assets are most commonly Lua scripts, using `Asset.Run` allows projects to be composed of multiple scripts.

# > Http

The Http library allows data to be retrieved and sent from websites. This opens up the possibility of leaderboards, asynchronous multiplayer games, cloud saves, integration of social services and interesting things of that sort.

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

> Here the data is the html page of "http://www.example.com".

`nil Http.Post(string url, HttpPostData postData, function OnSuccess, function OnFailure)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
url | string | The http address to contact. | ✘ |
postData | HttpPostData | Data to attach to the http request and send to the target webpage. | ✓  Default: nil
OnSuccess | function | A lua function that gets called on successfully contacting the target site. | ✘
OnFailure | function | A lua function that gets called on failing to contact the target site | ✘


When sending a POST request to a website `OnSuccess` is called if contact is successfully made with the website. `OnFailure` occurs if the request times out or there's a failure to contact the website. The `OnSuccess` function may be passed the information from the website as a string. `PostData` can be sent with the request, such as a highscore, or it may be nil if no postdata is required.

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

Creates a `HttpPostData` object. The encoding_type may be "application/x-www-form-urlencoded" or "multipart/form-data".

Generally it's best to use "multipart/form-data" but it also depends on the site you're sending the data to.

### application/x-www-form-urlencoded

The data is attached to the end of the URL

### multipart/form-data

The data is attached to the request in chunks.

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










