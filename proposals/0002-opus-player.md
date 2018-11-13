# ow-player

* Proposal: [YODA-0002](https://gitlab.rokid-inc.com/GravityTeam/yoda-evolution/blob/master/proposals/0002-opus-player.md)
* Authors: [lei.zhu](mailto:lei.zhu@rokid.com), [sudo](https://github.com/LanFly)
* Review Manager: [sudo](https://github.com/LanFly)
* Status: **Draft**

## Introduction

Replace the lightd player with a faster and less memory-intensive player.

## Motivation

Lightd is using the multimedia player, it takes up more memory and more disk space.
And have a fatal problem: Multimedia is multi-instance. we have to manually stop previous player.

## Proposed solution

Now the new player can only play audio in opus and wav formats.
And we have added an optional parameter: `ignore`. default value: `false`.

 - If the ignore parameter is true, it means that this audio does not need to be played when playing tts or media.
 - If the ignore parameter is false, it means that this audio should be played as tts, it will not be interrupted by the ignore parameter true.

We provide tools for converting your audio to opus format.

## Detailed design

2 apis hava changed.

- appSound: function(uri, options) => Promise
- sound: function(uri, options) => player

for example:

When playing network audio, we don’t need to play volume plus or minus audio.

So we should do this:

```js
// first play network_setup.opus
activity.appSound('path/to/network_setup.opus', { ignore: false })
  .then((res) => {
    // to do
  })
  .catch((err) => {
    // to do
  })

// then play volume_plus.wav
activity.appSound('path/to/volume_plus.wav', { ignore: true })
  .then((res) => {
    // to do
  })
  .catch((err) => {
    // to do
  })
```

## Effect on API compatibility

For application developers, the application only needs to make a little change, add the options parameter when calling the api.

For lighting effects developers, the audio will not stop automatically when the lighting effect is over.
If you need to stop the audio automatically when the lighting effect is stopped, you need to manually stop it in the stop hook function.

why lightd not stop the audio automatically when the lighting effect is stopped ?

Let me show you a case:

I want to play a light effect that turns on the microphone and plays a piece of audio.

```js
// The length of the audio is 2 seconds
light.sound('path/to/open_mic.wav')

// This operation is almost completed immediately.
light.fill(0, 0, 0)
light.render()
callback()
```

If lightd automatically turns off the audio, then the effect of this lighting effect is wrong.

I want to stop player when lighting effect is stopped, what should I do ?

```js
// The length of the audio is 2 seconds
var player = light.sound('path/to/open_mic.wav')

// This operation is almost completed immediately.
light.fill(0, 0, 0)
light.render()
callback()
return {
  stop: function () {
    player.stop()
  }
}
```

## How much performance has been improved?


## What changes have we made to the opus file format?


## How to use the opus format conversion tool?
