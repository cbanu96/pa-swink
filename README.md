# Pulse Audio Switch Sink

**P**ulse **A**udio **Sw**itch S**ink**, also known as *pa-swink*, is a
command-line tool which helps switch the default (fallback) sink and move any
currently active streams to the new sink.

This is a simple wrapper on top of *pactl*.

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

I usually place small tools like this one within `$HOME/.local/bin`:

```
	$ cp pa-swink ~/.local/bin
	$ cp samples/dmenu_pa-swink ~/.local/bin
```

## Usage

### Listing all sinks

**Syntax**: `pa-swink list`

**Example**:

```
	$ pa-swink list
	alsa_output.pci-0000_1c_00.1.hdmi-stereo
	alsa_output.usb-Razer_Razer_Kraken_USB-00.analog-stereo
```

### Switching to a new sink

**Syntax**: `pa-swink set <sink name>`

**Example**:

```
	$ pa-swink set alsa_output.pci-0000_1c_00.1.hdmi-stereo
	Setting default sink to alsa_output.pci-0000_1c_00.1.hdmi-stereo...
```

### Getting the current sink

**Syntax**: `pa-swink get`

**Example**:

```
	$ pa-swink get
	alsa_output.pci-0000_1c_00.1.hdmi-stereo
```

## Integration with dmenu (and i3)

The [samples/dmenu_pa-swink](../master/samples/dmenu_pa-swink) file is a
simple script showing how to use [dmenu](https://tools.suckless.org/dmenu/)
together with *pa-swink*.

In order to integrate this script with [i3](https://i3wm.org/), it's enough to
add the following line to `$HOME/.config/i3/config`:

```
	bindsym $mod+s exec --no-startup-id "dmenu_pa-swink"
```

## Integration with polybar

A simple approach to writing the currently active sink to a polybar module is
using `custom/script`:

```
	[module/pa-sink-description]
	type = custom/script
	exec = pactl list sinks | grep -A5 "Name: $(pa-swink get)" | grep Description | awk -F': ' '{print $2}'
```
