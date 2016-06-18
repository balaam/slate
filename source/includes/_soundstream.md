
# > SoundStream

Soundstream is for streaming music from the hard disk.

<aside class="warning">This library isn't implemented. All functions are just skeletons based on the Sound library.</aside>

## Play

Start playing the soundstream.

```lua
local id = SoundStream.Play("background_music", true)
```

`number SoundStream.Play(string name, boolean loop)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
name | string | The name of the soundstream as defined in the manfiest. | ✘
loop | boolean | If the soundstream should loop. | ✓ Default: false

The returned number is an id for the soundstream that can be used to alter it's volume or turn it off etc.

## Stop

Stop a soundstream.

`nil SoundStream.Stop(number id)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
id | number | The id of the sound stream. | ✘


## Pause

Pause a sound stream.

`nil SoundStream.Pause(number id)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
id | number | The id of the sound stream. | ✘

## Resume

Resume a paused sound stream.

`nil SoundStream.Resume(number id)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
id | number | The id of the sound stream. | ✘

## SetVolume

Set the volume of a sound stream, from 0 to 1.

`nil SoundStream.SetVolume(number id, number volume)`

Parameter |  Type | Description | Optional
--------- | ------- | ---- | ----
id | number | The id of the sound stream. | ✘
volume | number | The volume to set the sound stream. 0 to 1. | ✘
