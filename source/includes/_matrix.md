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

If no data is passed in then the matrix is initialised to the identity matrix.

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

This function updates a column inside a matrix.

`nil Matrix.SetColumn(Matrix m, int index, Vector v)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
m | Matrix | Matrix to update. | ✘
index | number | The matrix column to update 1 - 4. | ✘
v | Vector | The values to write into the column. | ✘

`nil Matrix.SetColumn(Matrix m, int index, number x, number y, number z, number w)`

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

`nil Matrix.SetRotation(Matrix m, Vector axis, number angle)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
m | Matrix | The matrix to write the rotation data to. | ✘
axis | Vector | The normal vector to rotate around. | ✘
angle | number | The amount of rotation to apply in degrees. | ✘

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
