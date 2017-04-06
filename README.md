# Midi Driver [![Build Status](https://travis-ci.org/billthefarmer/mididriver.svg?branch=master)](https://travis-ci.org/billthefarmer/mididriver) [![](https://jitpack.io/v/billthefarmer/mididriver.svg)](https://jitpack.io/#billthefarmer/mididriver)

Android midi driver using Sonivox EAS library. The library is
available in
[Releases](https://github.com/billthefarmer/mididriver/releases).

Licensed under GPL or Apache license - your choice.

Includes Sonivox EAS library rebuilt without spurious references to
libutils and libcutils. The ARM versions have been build with the
assembler source files.

Google have fixed the 64 bit reverb bug:
[#15](https://github.com/billthefarmer/mididriver/issues/15) -
[Fix math functions for 64-bit](https://github.com/android/platform_external_sonivox/commit/d216e303f65f5e36ffba92d342a8c61f753c98d7). The
driver now works correctly on 64 bit devices.

The [MidiTest](https://github.com/billthefarmer/miditest) app is now
in a separate repository.

Add the driver to your build.gradle with
```gradle
allprojects {
  repositories {
    jcenter()
    maven { url "https://jitpack.io" }
  }
}
```
and:
```gradle
dependencies {
  compile 'com.github.billthefarmer:mididriver:v1.12'
}
```
### Methods

	void start()  Start the driver. Call from onResume().

	void stop()  Stop the driver. Call from onPause();

	void addOnMidiStartListener(OnMidiStartListener l);

	void queueEvent(byte[]) Send a midi message. This method now just
    calls write()

#### Listener

	void onMidiStart() This is called when the driver has started so
    that program change messages, etc may be sent. This is now
    somewhat redundant but has been left in.

### Native Methods

	boolean init()  Return true on success, or false on failure.
	
	int[] config()  Return a four element array of ints with part of
	the EAS onfig:

      config[0] = pLibConfig->maxVoices;
      config[1] = pLibConfig->numChannels;
      config[2] = pLibConfig->sampleRate;
      config[3] = pLibConfig->mixBufferSize;

	boolean write(byte buffer[])  Writes midi data to the Sonivox
	synthesizer. The length of the array should be the exact length of
	the message or messages. Returns true on success, false on
	failure.

	boolean shutdown()  Shut down the synthesizer. Returns true on
	success, false on failure.
