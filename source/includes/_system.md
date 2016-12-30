# > System

System functions control how the game is displayed and interacts with  the host operating system.

## Exit

This call closes down the application. Want to implement a Quit button? This is what you're after.

`nil System.Exit()`

## IsWideScreen

This a dummy function that will always return true.

`boolean System.IsWideScreen()`

## OpenURL

Opens a URL in the default webbrowser.

```lua
System.OpenURL("http://dinodeck.com")
```

`nil System.OpenURL(string url)`

<aside class="warning">Only works on windows currently!</aside>

## ScreenTopLeft

Get the the top left position of the screen in pixels. (Equivalent to: `-ScreenWidth()/2, ScreenHeight`).

`Vector System.ScreenTopLeft()`

## ScreenBottomRight

Get the the bottom right position of the screen in pixels. (Equivalent to: `ScreenWidth()/2, -ScreenHeight`).

`Vector System.ScreenBottomRight()`

## ScreenHeight

Get the height of the screen in pixels.

`number ScreenHeight()`

## ScreenWidth

Get the width of the screen in pixels.

`number ScreenWidth()`

## Version

Returns the current version of Dinodeck as a string.

`string Version()`

```lua
local version = System.Version()
print(version) -- "v1.1.2"
```
