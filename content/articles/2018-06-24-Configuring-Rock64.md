Title: Setting up linux in Rock64 SBC for the first time
date: 2018-06-24 17:16
comments: true
slug: configuring-rock64
tags: linux,arm,pine64,rock64,sbc,alsa,audio,mediacenter,microserver,server,arm64,ubuntu,bionic

I recently purchased a [Rock64](https://www.pine64.org/?page_id=7147) SBC (from
pine64),
which is a fairly powerful and inexpensive micro computer. You can think 
of it as a more powerful alternative to the famous raspberry pi (to date).
The idea is setting this up as a media center for my home and as a micro
server, for storing my personal projects in repositories and similar. I 
also acquired a eMMC module which I haven't tested yet because I have to
wait for the serial-USB converter thing to arrive, once I get my hands into
this I will let you know in a future blog post.

# Installing Linux into SD and first steps

As you could guess, flashing linux into the SD is pretty straightforward,
to avoid complications I just used [ayufan's images](https://github.com/ayufan-rock64/linux-build/releases)
which are already configured to work on the Rock64 SBC. I do have to tell
that I had better results using the ubuntu bionic-lxde image for 
rock64/arm64. I tried with the minimal bionic image but had performance 
issues that I did not experienced with the lxde one. One of the main reasons
for choosing this image is that the experimental hardware acceleration when
playing videos allegedly works better with this image.

To flash the SD you just download the desired image in `*.img.xz` format
from the ayufan's repository (link above), insert the SD into your laptop, or
whatever device you will be using to flash it, and then use a software to
flash it. In my case I found the software [Etcher](https://etcher.io/) really
easy and complete enough to use. You **may** have Etcher available in your
linux package system (I know it's in Solus, which is the Linux distribution
I'm using). The process of using Etcher is pretty straightfoward, you just 
look for the image file, select the SD/SD-reader and click "Flash", it takes
some minutes depending on your SD and system. Take into account that Etcher
is also available for Windows and Mac.

After it completes, you just plug the microSD into the Rock64 board and 
turn it on either by plugging it to power or pushing the power button on
it. It will load the Linux image from SD automatically. You will then get
a login display which you can use `rock64` for both user and password and
this will end up loading the [LXDE](https://lxde.org/) desktop environment.

# Getting sound to work

After installing and booting Ubuntu image, everything worked as expected 
except for the sound. As sonn as I logged into the desktop graphical environment
I could hear some noises coming from the speakers of the TV that was connected
to the Rock64 but no sound, at all, after that. What I thought was that
[pulseaudio](https://www.freedesktop.org/wiki/Software/PulseAudio/) somehow
was not working fine in this architecture, therefore I thought of disabling 
it completely and letting the system use only [ALSA](https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture),
which is built into the kernel. This was the solution indeed and what I did
to disable and set up alsa was as follows:

* Disable pulseaudio for the user (it's not recommeded to uninstall it, 
disabling it should be enough), by following instruction on [this site](https://kodi.wiki/view/PulseAudio/HOW-TO:_Disable_PulseAudio_and_use_ALSA_%28without_removing_PulseAudio%29_for_Ubuntu),
which was done by running the following instructions:
1. `cp /etc/pulse/client.conf /home/yourusername/.config/pulse`
2. Edit the file such that the line with `; autospawn = yes` changes to
   `autospawn=no` (note there isn't a semicolon at the beggining of the line).

* After disabling `pulseaudio` the only thing that's missing is configuring ALSA
to use HDMI as the audio output. This is done by creating the file
`/etc/asound.conf` with the following content inside it:
```
pcm.!default {
    type             plug
    slave.pcm       "rock_audio_pot"
}

pcm.rock_audio_pot {
    type            softvol
    slave {
        pcm         "hw:1"
    }
    control {
        name        "Master"
        card        0
    }
}
```

After this you should just reboot/restart the system.

# 3D accelerated video playback

As told in [ayufan's site](https://github.com/ayufan-rock64/linux-build/blob/master/recipes/video-playback.md),
the ubuntu bionic image comes with rkmpv which is a wrapper for mpv to make it
use the hardware/GPU acceleration, such that you should only run the following
command to play a video in your screen, using the GPU acceleration

```
rkmpv file.mkv
```

What I found out is that rkmpv only sets up a specific environment variable and
passes some specific parameters to mpv to play the file, I thought on making
them the default for my setup, this is achieved by doing the following.

First you have to edit your `~/.bashrc` file in your (for example by running
`nano ~/.bashrc`), and append to the end of the file the following line

```
export LD_LIBRARY_PATH=/usr/lib/aarch64-linux-gnu/gbm:/usr/lib/arm-linux-gnueabihf/gbm
```

save and close it.

Then you just need to tell mpv to use the expected parameters as default
parameters, this is done by creating a file in `~/.config/mpv/mpv.conf` with the
following content

```
vo=gpu
gpu-context=drm
hwdec=rkmpp
```

This will just make mpv use these parameters by default when it's run without
manually specified parameters/options.

# Conclusion

This basically resulted in what I need so far for the Rock64, which is a basic
media center and linux TV, there are some other things I wanted to install to
play with it, such as installing tools like [peerflix](https://github.com/mafintosh/peerflix), 
[torrentflix](https://github.com/ItzBlitz98/torrentflix) or [kodi](https://kodi.tv/).

# Troubleshooting

I did encounter some other problems, specifically the bionic-minimal image from
ayufan didn't work as expected. I tried installing `LXQT` environment without any
luck, all I got was a black screen. Then, I also tried using `budgie-wm` which
did load but the performance was very poor. Still I tried to set up mpv, for
video playback, and all the other tools without much luck. This was what finally
made me choose to use the Ubuntu bionic-lxde image, which ended up working
pretty well.
