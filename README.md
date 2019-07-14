# Pulse Audio Switch Sink

**P**ulse **A**udio **Sw**itch S**ink**, also known as *pa-swink*, is a
command-line tool which helps switch the default (fallback) sink and move any
currently active streams to the new sink.

This is a simple wrapper on top of *pactl* and *pacmd*.

## Motivation

I did not find any easy way to switch between various audio devices using
tools such as `pavucontrol`.

I wanted to create a tool that is as easy to use as the one Windows provides,
albeit involving no silly mouse-waving and a tiny amount of keystrokes.

The main use case, personally, is switching between speakers and headphones
without having to manually migrate streams to use the new sink in the
`pavucontrol` UI.

## Installation

Place the provided shell script wherever you want and use it however you like.
An example of integration in a window manager such as i3 is provided below.

## Usage

### Listing all sinks

`pa-swink list` displays the sinks' names, as such:

```
	$ pa-swink list
	alsa_output.pci-0000_1c_00.1.hdmi-stereo
	alsa_output.usb-Razer_Razer_Kraken_USB-00.analog-stereo
```

### Switching to a new sink

`pa-swink set <sink name>`

```
	$ pa-swink set alsa_output.pci-0000_1c_00.1.hdmi-stereo
	Setting default sink to alsa_output.pci-0000_1c_00.1.hdmi-stereo...
```

### Getting the current sink

`pa-swink get`

```
	$ pa-swink get
	alsa_output.pci-0000_1c_00.1.hdmi-stereo
```

## Integration with dmenu (and i3)

**TODO**: This is in progress.

## Integration with polybar

**TODO**: This is in progress.
