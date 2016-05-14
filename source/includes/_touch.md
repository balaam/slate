
# > Touch

The touch library is for touch input, such as a mobile phone screen.

## Held

Is the user pressing their finger against the touchpad.

`boolean Touch.Held()`

Returns true if held, otherwise false.

## JustPressed

Has the user touched the pad for the first time.

`boolean Touch.JustPressed()`

Returns true if just pressed, otherwise false.

## JustReleased

Has the user released their press of the touch screen.

`boolean Touch.JustReleased()`

Returns true if just released the press otherwise false.

## Position

Gets the last position of the touch as a vector. Starts at 0, 0.

`Vector Touch.Position()`

`void Touch.Position(Vector v)`

## X

Gets the last X position of the touch.

`number Touch.X()`

## Y

Gets the last Y position of the touch.

`number Touch.Y()`