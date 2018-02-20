# Mixing video (GStreamer command-line cheat sheet)

### Picture in picture

Here we have two source (mp4) files, which should be set as environment variables `$SRC` and `$SRC2`

```
gst-launch-1.0   \
    filesrc location="$SRC2" ! \
    decodebin ! videoconvert ! \
    videoscale ! video/x-raw,width=640,height=360 ! \
    videomixer name=mix sink_0::alpha=1 sink_1::alpha=1 !   \
    videoconvert ! autovideosink \
    filesrc location="$SRC" ! \
    decodebin ! videoconvert ! \
    videoscale ! video/x-raw,width=320,height=180! \
    mix.
```

Put a box around the in-picture using ‘videobox’ e.g.

```
gst-launch-1.0   \
    filesrc location="$SRC2" ! \
    decodebin ! videoconvert ! \
    videoscale ! video/x-raw,width=640,height=360 ! \
    videomixer name=mix sink_0::alpha=1 sink_1::alpha=1 !   \
    videoconvert ! autovideosink \
    filesrc location="$SRC" ! \
    decodebin ! videoconvert ! \
    videoscale ! video/x-raw,width=320,height=180! \
    videobox border-alpha=0 top=-10 bottom=-10 right=-10 left=-10 ! \
    mix.
```

Choose where the in-picture goes with the ‘xpos’ and ‘ypos’ attributes of videomixer, e.g.

```
gst-launch-1.0   \
    filesrc location="$SRC2" ! \
    decodebin ! videoconvert ! \
    videoscale ! video/x-raw,width=640,height=360 ! \
    videomixer name=mix sink_0::alpha=1 sink_1::alpha=1 sink_1::xpos=50 sink_1::ypos=50 !   \
    videoconvert ! autovideosink \
    filesrc location="$SRC" ! \
    decodebin ! videoconvert ! \
    videoscale ! video/x-raw,width=320,height=180! \
    mix.
```
