# > Vector

A Vector class. It has four elements: XYZW. It's used for physics simulations and math stuff. The vector is also used as a simple way to hold a color where XYZW is treated as RGBA.

## Add

Adds two vectors together, or adds a number to all vector values.

```lua
local v1 = Vector.Create(0, 0, 0, 1)
local v2 = Vector.Create(1, 1, 1, 1)

Vector.Add(v1, v2) -- (1, 1, 1, 2)
v1:Add(v2) -- (1, 1, 1, 2)

Vector.Add(v2, 1) -- (2, 2, 2, 2)
v1:Add(1) -- (1, 1, 1, 2)

```

`Vector Vector.Add(Vector v1, Vector v2)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
v1 | Vector | The first vector to add. | ✘
v2 | Vector | The second vector to add | ✘

`Vector Vector.Add(Vector v1, float n)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
v1 | Vector | The first vector to add. | ✘
n | number | Number to add to each of the vector's elements | ✘

## Copy

Copies the data from one Vector to another.

```lua
local v1 = Vector.Create(0, 0, 0, 1)
local v2 = Vector.Create(1, 1, 1, 1)

v1:Copy(v2)
print(v1) -- (1, 1, 1, 1)
Vector.Copy(v2, Vector.Create(5, 4, 3, 2))
print(v2) -- (5, 4, 3, 2)
```

`Vector Vector.Copy(Vector to, Vector from)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
to | Vector | The vector that will have it data overriden. | ✘
from | Vector | The vector to copy the new data from. | ✘

## Create

Create a new Vector.

```lua
local v = Vector.Create()
print(v) -- (0, 0, 0, 0)

local source = Vector.Create(1, 2, 3, 4)
local s2 = Vector.Create(source)

print(s2) -- (1, 2, 3, 4)

```

`Vector Vector.Create()`

With no arguments an empty vector with all elements set to zero is returned.

`Vector Vector.Create(float x, float y, float z, float w)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
x | number | The x element for the vector. | ✓ Default: 0
y | number | The y element for the vector. | ✓ Default: 0
z | number | The z element for the vector. | ✓ Default: 0
w | number | The w element for the vector. | ✓ Default: 0

`Vector Vector.Create(Vector source)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
source | Vector | A new vector is created copying all the data from the source. | ✘

## Cross

Performs the cross product on two vectors. If you imagine the two vectors making a plane, the cross product gives the normal for that plane.

`void Vector.Cross(Vector destination, Vector left, Vector right)`

```lua
local xAxis = Vector.Create(1, 0, 0, 0)
local zAxis = Vector.Create(0, 0, 1, 0)
output = Vector.Create()

Vector.Cross(output, xAxis, zAxis)
print(output) -- (0, 1, 0, 0)
```

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
destination | Vector | The vector to store the result in. | ✘
left | Vector | The left vector of the cross. | ✘
right | Vector | The right vector of the cross. | ✘

## Divide

The left vector's elements are divided by the right and stored in the destination vector.

`void Vector.Divide(Vector destination, Vector left, Vector right)`

```lua
local a = Vector.Create(2, 4, 6, 8)
local b = Vector.Create(2, 2, 2, 2)
output = Vector.Create()

Vector.Divide(output, a, b)
print(output) -- (1, 2, 3, 4)
```

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
destination | Vector | The vector to store the result in. | ✘
left | Vector | The left vector of the divide. | ✘
right | Vector | The right vector of the divide. | ✘

## Dot2

Performs a dot product on the X, Y elements for the vector. The dot product calculates the cosine of the angle between two vectors.

```lua
a = Vector.Create(0, 1, 0, 0)
b = Vector.Create(0, -1, 0, 0)
output = Vector.Dot2(a, b)
print(output) -- -1
```

Values range from 1 to -1. If the two input vectors are pointing in the same direction, then the return value will be 1. If the two input vectors are pointing in opposite directions, then the return value will be -1.

`void Vector.Dot2(Vector a, Vector b)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
left | Vector | The left vector of the dot. | ✘
right | Vector | The right vector of the dot. | ✘

## Dot3

Performs the dot product on the X, Y, Z elements of two vectors. Otherwise the same as Dot2.

## Dot4

Performs the dot product on the X, Y, Z, W elements of two vectors.  Otherwise the same as Dot2.

## Length2

Returns the length of a vector, only taking into account the X and Y elements.

```lua
a = Vector.Create(0, 1, 0, 0)
length = a:Length2()
print(length) -- 1
```

`void Vector.Length2(Vector v)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
v | Vector | The vector to calculate the length from. | ✘

## Length3

Same as Length2 but operates on the X, Y and Z elements.

## Length4

Same as Length4 but operates on the X, Y and Z elements.

## Multiply

Multiply the elements of one vector with another.

```lua
a = Vector.Create(0, 1, 0, 0)
b = Vector.Create(1, 1, 1, 1)
c = Vector.Create()
Vector.Multiply(c, a, b)

print(c) -- 0, 1, 0, 0
```

`void Vector.Multiply(Vector destination, Vector left, Vector right)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
destination | Vector | The vector to store the result in. | ✘
left | Vector | The left vector of the mutiply. | ✘
right | Vector | The right vector of the mutiply. | ✘


## Normalize2

Normalize the vector to a unit vector. Only considers the X, Y elements

## Normalize3

Normalize the vector to a unit vector. The same as Normalize2 but for X, Y, Z

## Normalize4

Normalize the vector to a unit vector. The same as Normalize3 but for X, Y, Z, W.

## SetBroadcast

Set every element of the vector to the same value.

```lua
a = Vector.Create(1, 2, 3, 4)
a:SetBroadcast(2)

print(a) -- 2, 2, 2, 2
```

`void Vector.SetBroadcast(Vector vector, number value)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
v | Vector | The vector to write to. | ✘
value | Vector | The number to write into the vector. | ✘


## SetXyzw

Sets the X, Y, Z and W elements of the vector.

## SetX

Set the X value for a vector.

`number Vector.SetX(Vector vector, number value)`

```lua
Vector v = Vector.Create(0, 0, 0, 0)
v:SetX(20)
print(v:X()) -- 20
```

## SetY

Set the Y value for a vector.

`number Vector.SetY(Vector vector, number value)`

```lua
Vector v = Vector.Create(0, 0, 0, 0)
v:SetY(20)
print(v:Y()) -- 20
```

## SetZ

Set the Z value for a vector.

`number Vector.SetZ(Vector vector, number value)`

```lua
Vector v = Vector.Create(0, 0, 0, 0)
v:SetZ(20)
print(v:Z()) -- 20
```

## SetW

Set the W value for a vector.

`number Vector.SetW(Vector vector, number value)`

```lua
Vector v = Vector.Create(0, 0, 0, 0)
v:SetW(20)
print(v:W()) -- 20
```

## Subtract

Subtract two vectors.

```lua
local v1 = Vector.Create(0, 0, 0, 1)
local v2 = Vector.Create(1, 1, 1, 1)

Vector.Subtract(v1, v2) -- (-1, -1, -1, 0)
v1:Subtract(v2) -- (-1, -1, -1, 0)
```

`Vector Vector.SetW(Vector v1, Vector v2)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
v1 | Vector | First vector to subtract. | ✘
v2 | Vector | Second vector to subtract from first | ✘

## X

Get the X element for a vector.

`number Vector.X(Vector vector)`

```lua
Vector v = Vector.Create(1, 2, 3, 0)
print(v:X()) -- 1
```

## Y

Get the Y element for a vector.

`number Vector.Y(Vector vector)`

```lua
Vector v = Vector.Create(1, 2, 3, 0)
print(v:Y()) -- 2
```

## Z

Get the Z element for a vector.

`number Vector.Z(Vector vector)`

```lua
Vector v = Vector.Create(1, 2, 3, 0)
print(v:Z()) -- 3
```

## W

Get the W element for a vector.

`number Vector.W(Vector vector)`

```lua
Vector v = Vector.Create(1, 2, 3, 0)
print(v:W()) -- 0
```

## __add

A metatable entry for infix addition. Uses the `Add` function.

```lua
a = Vector.Create(1,1,1,1)
b = Vector.Create(a)
print(a + b) -- 2,2,2,2
```

## __div

A metatable entry for infix division. Uses the `Divide` function.

```lua
a = Vector.Create(1,1,1,1)
b = Vector.Create(2,2,2,2)
print(a / b) -- 0.5, 0.5, 0.5, 0.5
```

## __mul

A metatable entry for infix multiplication. Uses the `Multiply` function.

```lua
a = Vector.Create(1,1,1,1)
b = Vector.Create(2,2,2,2)
print(a * b) -- 2, 2, 2, 2
```

## __sub

A metatable entry for infix subtraction. Uses the `Subtract` function.

```lua
a = Vector.Create(1,1,1,1)
b = Vector.Create(2,2,2,2)
print(a - b) -- -1, -1, -1, -1
```

## __tostring

A metatable entry for writing to a string.

```lua
print(Vector.Create())
-- Ouputs:
-- Vector.Create(0, 0, 0, 0)
```

## __unm

A metatable entry for adding a minus to the front of the vector to negate it.

```lua
a = -Vector.Create(1, 1, 1, 1)
print(a) -- -1, -1, -1, -1
```
