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

`boolean Keyboard.Held( number keyCode)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
keyCode  | number | The key to check if held. Refer to the table in the Keyboard Library for a full lisitng of key codes. | ✘

Returns true if the key is currently being pressed.

## JustReleased

`boolean Keyboard.JustReleased( number keyCode )`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
keyCode  | number | The key to check if held. Refer to the table in the Keyboard Library for a full lisitng of key codes. | ✘

Returns true if the key was released during the previous frame.

## JustPressed

`boolean Keyboard.JustPressed( number keyCode )`

Returns true if the key was pressed during the previous frame.

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
keyCode  | number | The key to check if held. Refer to the table in the Keyboard Library for a full lisitng of key codes. | ✘

