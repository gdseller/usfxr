usfxr
=====

usfxr is a C# library to generate and play audio effects in real time inside a Unity game. With usfxr, one can easily synthesize audio for typical game-related actions such as item pickups, jumps, lasers, hits, explosions, and more.

It is a Unity-compatible C# port of Thomas Vian's [as3sfxr](https://code.google.com/p/as3sfxr/), which itself is an ActionScript 3 port of Tomas Pettersson's [sfxr](http://www.drpetter.se/project_sfxr.html).

Despite my name not being Thomas or a variant of it, I found myself wishing for a (free) library to procedurally generate audio inside Unity in real time, and usfxr is the result.


Introduction
------------

First things first: if you're just looking for a few good 16 bit-style sound effects to use in games, anyone can use sound files generated by [the original sfxr](http://www.drpetter.se/project_sfxr.html) or [as3sfxr's online version](http://www.superflashbros.net/as3sfxr/) without any changes, since both applications generate audio files.

However, by using a runtime library like usfxr (inspired by as3sfxr), you can generate the same audio samples in real time, or re-synthesize effects generated in any of those tools by using a small list of parameters (a short string). The advantages of this approach are twofold:

* Audio is generated in real time; there's no storage of audio files as assets necessary, making compiled project sizes smaller
* Easily play variations of every sound (like jumps); adds more flavor to the gameplay experience

I make no claims in regards to the source code or interface, since it was simply adapted from Thomas Vian's own code and (elegant) interface. As such, usfxr contains the same features offered by as3sfxr, such as caching of generated audio and ability to play sounds with variations. But because it is adapted to work on a different platform, however, it has advantages of its own:

* Fast audio synthesis
* Ability to cache sounds the first time they're needed
* Completely asynchronous caching and playback; sound is generated on a separate, non-blocking thread with minimal impact on gameplay
* Minimal setup necessary; full code-based solution


Installation
------------


Usage
-----



Interface
---------



Samples
-------



-------

TODO:
* Test if SfxrParams.pow() is actually faster than using pow
* Test if SfxrParams.to4DP() is returning numbers correctly (1.00001 becomes 1.00000, etc) - maybe round it?
* Replace Random.value with a different function? The original used Math.random(), which returns 0 <= n < 1, while Random.value returns 0 <= n <= 1
* if float.parse(str) already returns 0 on empty strings, so SfxrParams.setSettingsString() can be simpler and faster
* replace getTimer() on SfxrSynth with a Time specific call?
* Decide on a better name for "paramss"
* Too many potential conversions between uint/int - move everything to int?

* Line 496 of SfxrSynth: awkward conversion (was implying from float to int): _changeLimit = (int)((1f - p.changeSpeed) * (1f - p.changeSpeed) * 20000f + 32f);
* Line 682 of SfxrSynth: awkward conversion (was implying from float to int): _phase = _phase - (int)_periodTemp;
* Line 552 of SfxrSynth: awkward conversion: _envelopeFullLength was originally a float, but used as an uint everywhere else, so I'm doing the conversion earlier. what kind of unit is this? it may be cutting the audio short
* Line 262 of SfxrSynth: test filling of data samples to see what's faster

* Re-enable other functions on SfxrSynth that have been temporarily disabled - search for [[disabled]]
* Search for (uint) casts -- too many...

* Re-enable wav file generation? turn on getWavFile(), and allow waveData false on synthWave() on SfxrSynth

Missing aspects:
* events/callbacks


Features:
* Use Coroutines/yield to asynchronously create the data?