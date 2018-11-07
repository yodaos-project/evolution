# opus-player

* Proposal: [YODA-0002](https://gitlab.rokid-inc.com/GravityTeam/yoda-evolution/blob/master/proposals/0002-opus-player.md)
* Authors: [sudo](https://github.com/LanFly), [lei.zhu](mailto:lei.zhu@rokid.com)
* Review Manager: TBD
* Status: **Drafting**

*During the review process, add the following fields as needed:*

* Implementation: [rokid/yodaos#NNNNN](https://github.com/rokid/yodaos/pull/NNNNN)
* Decision Notes: [Rationale](https://forums.yodaos.org/), [Additional Commentary](https://forums.yodaos.org/)
* Bugs: [BUG-NNNN](https://bugs.yodaos.org/browse/BUG-NNNN), [BUG-MMMM](https://bugs.yodaos.org/browse/BUG-MMMM)
* Previous Revision: [1](https://github.com/rokid/yoda-evolution/blob/...commit-ID.../proposals/NNNN-filename.md)
* Previous Proposal: [YODA-XXXX](XXXX-filename.md)

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

The application only needs to make a little change, add the options parameter when calling the api.

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

## Alternatives considered

nothing now
