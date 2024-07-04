# Human in video

I needed a quick and simple CLI tool for finding humans in videos...

and optionally creating an output video with chapters placed at an occurrence
of a human.

Uses the cv2 lib and 'haarcascade_upperbody.xml'. You could change this in the
script to some other model. This would allow one to match on anything really.

I use `mpv` and the keyboard shortcuts `page-up` and `page-down` to jump between
chapters. You could use VLC for the same goals.

## Usage

> For demonstration purposes we are using an image instead as it saves on repo
> size.

Requires a video as an argument.

```bash
human-in-video
```
```
usage: human-in-video [-h] input_video [output_video]
human-in-video: error: the following arguments are required: input_video
```

Will exit non zero when no humans are found.

```bash
human-in-video ./no-human.jpg
```
```
INFO - Starting to process video: ./no-human.jpg
INFO - Finished processing video. Total frames: 1, Chapters detected: 0
ERROR - No humans detected in the video.
```

Exits with exit-code 0 when a human is found.

```bash
human-in-video ./human.jpg
```
```
INFO - Starting to process video: ./human.jpg
INFO - Human detected at frame 0, timestamp 0.00s
INFO - Human detected, exiting.
```

Exits with exit-code 0 and creates an output video with chapters.

```bash
human-in-video ./human.jpg ./human-output.jpg
```
```
INFO - Starting to process video: ./human.jpg
INFO - Human detected at frame 0, timestamp 0.00s
INFO - Finished processing video. Total frames: 1, Chapters detected: 1
INFO - Chapters file created: /tmp/tmp639jc2te.txt
INFO - Starting to create video with chapters: ./human-output.jpg
ffmpeg version 4.2.7-0ubuntu0.1 Copyright (c) 2000-2022 the FFmpeg developers
  built with gcc 9 (Ubuntu 9.4.0-1ubuntu1~20.04.1)
  configuration: --prefix=/usr --extra-version=0ubuntu0.1 --toolchain=hardened --libdir=/usr/lib/x86_64-linux-gnu --incdir=/usr/include/x86_64-linux-gnu --arch=amd64 --enable-gpl --disable-stripping --enable-avresample --disable-filter=resample --enable-avisynth --enable-gnutls --enable-ladspa --enable-libaom --enable-libass --enable-libbluray --enable-libbs2b --enable-libcaca --enable-libcdio --enable-libcodec2 --enable-libflite --enable-libfontconfig --enable-libfreetype --enable-libfribidi --enable-libgme --enable-libgsm --enable-libjack --enable-libmp3lame --enable-libmysofa --enable-libopenjpeg --enable-libopenmpt --enable-libopus --enable-libpulse --enable-librsvg --enable-librubberband --enable-libshine --enable-libsnappy --enable-libsoxr --enable-libspeex --enable-libssh --enable-libtheora --enable-libtwolame --enable-libvidstab --enable-libvorbis --enable-libvpx --enable-libwavpack --enable-libwebp --enable-libx265 --enable-libxml2 --enable-libxvid --enable-libzmq --enable-libzvbi --enable-lv2 --enable-omx --enable-openal --enable-opencl --enable-opengl --enable-sdl2 --enable-libdc1394 --enable-libdrm --enable-libiec61883 --enable-nvenc --enable-chromaprint --enable-frei0r --enable-libx264 --enable-shared
  libavutil      56. 31.100 / 56. 31.100
  libavcodec     58. 54.100 / 58. 54.100
  libavformat    58. 29.100 / 58. 29.100
  libavdevice    58.  8.100 / 58.  8.100
  libavfilter     7. 57.100 /  7. 57.100
  libavresample   4.  0.  0 /  4.  0.  0
  libswscale      5.  5.100 /  5.  5.100
  libswresample   3.  5.100 /  3.  5.100
  libpostproc    55.  5.100 / 55.  5.100
Input #0, image2, from './human.jpg':
  Duration: 00:00:00.04, start: 0.000000, bitrate: 30885 kb/s
    Stream #0:0: Video: mjpeg (Baseline), yuvj420p(pc, bt470bg/unknown/unknown), 960x641 [SAR 1:1 DAR 960:641], 25 tbr, 25 tbn, 25 tbc
Input #1, ffmetadata, from '/tmp/tmp639jc2te.txt':
  Duration: 00:16:40.00, start: 0.000000, bitrate: N/A
    Chapter #1:0: start 0.000000, end 1000.000000
Output #0, image2, to './human-output.jpg':
  Metadata:
    encoder         : Lavf58.29.100
    Chapter #0:0: start 0.000000, end 1000.000000
    Stream #0:0: Video: mjpeg (Baseline), yuvj420p(pc, bt470bg/unknown/unknown), 960x641 [SAR 1:1 DAR 960:641], q=2-31, 25 tbr, 25 tbn, 25 tbc
Stream mapping:
  Stream #0:0 -> #0:0 (copy)
Press [q] to stop, [?] for help
frame=    1 fps=0.0 q=-1.0 Lsize=N/A time=00:00:00.04 bitrate=N/A speed= 110x    
video:151kB audio:0kB subtitle:0kB other streams:0kB global headers:0kB muxing overhead: unknown
INFO - Video with chapters created: ./human-output.jpg
```

Let's cleanup.

```bash
rm  ./human-output.jpg
```

Happy coding!
