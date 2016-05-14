# > SaveGame

Dinodeck supports extremely simple saving. On PC and Mac a save game file save.dat will be written to the same directory when the save game is written. To save the Lua data the data needs serialising to a string.

## Create

Create the save game object.

`SaveGame SaveGame.Create()`

## Read

Read the save game as a string.

`string SaveGame.Read(SaveGame saveGame)`

```lua
local data = someSave:Read()
print("Save data: ", data)
```

## Write

Write a Lua string to the save game. This overwrites any existing save game.

`nil SaveGame.Write(SaveGame saveGame, string data)`

```lua
local someSave = SaveGame.Create()
someSave:Write("{level_unlocked = 1}")
```