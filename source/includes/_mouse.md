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

The X, Y position of the mouse returned as a `Vector`. The z coordinate is 0.

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

If a mouse button has just been pressed and then released.

`bool Mouse.JustReleased(int mouseButton)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
mouseButton | int | The mouse button to test either left, middle or right. | ✘

```lua
if Mouse.JustReleased(MOUSE_BUTTON_LEFT) then
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
-- Draws "Hello World" next to the mouse position.
gRenderer = Renderer.Create()
if Mouse.Held(MOUSE_BUTTON_LEFT) then
    local pos = Mouse.Position()
    gRenderer:DrawText2d(pos:X(), pos:Y(), "Hello World")
end
```