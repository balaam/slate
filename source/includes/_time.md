# > Time

Time and date code is notoriously tricky but luckily this library is here to help out.

## Difference

Returns the difference between two times in seconds.

`number Time.Difference(number time1, number time2)`

```lua
LoadLibrary("Renderer")
LoadLibrary("Time")

gRenderer = Renderer:Create()

start = Time.GetTime()

function update()

    local now = Time.GetTime()
    local runTimeSecs = Time.Difference(start, now)

    gRenderer:AlignText("right", "center")
    gRenderer:DrawText2d(-5, 0, "Program Has Been Running For:")
    gRenderer:AlignText("left", "center")
    gRenderer:DrawText2d(5, 0, string.format("%ds", runTimeSecs))
end
```

## GetDate

Returns the date, in the range 1-31, from a raw time number.

`number GetDate(number time)`

```lua
local now = Time.GetTime()
print(Time.GetDate(now)) -- a number representing the date
```


## GetDay

Returns the day, in the range 1-7, from a raw time number.

```lua
local now = Time.GetTime()
print(Time.GetDay(now)) -- a number representing the day
```

`number GetDay(number time)`

## GetHour

Returns the hour of the day from a raw time number. In the range 0 - 23.

```lua
local now = Time.GetTime()
print(Time.GetHour(now)) -- a number representing the hour
```

`number GetHour(number time)`

## GetMinute

Returns the current minute of the time from a raw time number. (This not the time in minutes, it's the minute value of the current time. i.e. if the time ends in 4:03 this function returns 3.)

The range returned is 0 - 59.

`number GetMinute(number time)`

## GetMonth

Gets the month from a raw time string. The range is 1-12.

`number GetMonth(number time)`

## GetSecond

Get the second value for the current time.


## GetTime

Get the raw time string for the current date and time.

```
local time = Time.GetTime()
print("It's the year %s", Time.GetYear(time))
```

`number GetTime()`


## GetYear

Get the year for the current raw string.

`number GetYear(number time)`




