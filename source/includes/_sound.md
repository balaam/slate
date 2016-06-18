# > Sound

Play a sound definied in the manifest. Only .wavs are supported.

## Play

Play a sound.

```lua
local id = Sound.Play("button_press", false)
```

`number Sound.Play(string name, boolean loop)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
name | string | The name of the sound as defined in the manifest. | ✘
loop | boolean | If the sound should loop. | ✓ Default: false

The play function returns an `id` that can be used to control the sound.

## Stop

Stop a sound.

`nil Sound.Stop(number id)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
id | number | The id of the sound. | ✘

## Pause

Pause a sound.

`nil Sound.Pause(number id)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
id | number | The id of the sound. | ✘

## Resume

Resume a paused sound.

`nil Sound.Resume(number id)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
id | number | The id of the sound. | ✘

## SetVolume

Set the volume of a sound, from 0 to 1.

`nil SoundSetVolume(number id, number volume)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
id | number | The id of the sound. | ✘
volume | number | The volume to set the sound. 0 to 1. | ✘
