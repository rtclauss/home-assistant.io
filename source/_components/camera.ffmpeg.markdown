---
layout: page
title: "FFmpeg Camera"
description: "Instructions on how to integrate a video feed via FFmpeg as a camera within Home Assistant."
date: 2016-08-13 08:00
sidebar: true
comments: false
sharing: true
footer: true
logo: ffmpeg.png
ha_category: Camera
ha_release: 0.26
ha_iot_class: Local Polling
---

The `ffmpeg` platform allows you to use any video feed as a camera in Home Assistant via [FFmpeg](http://www.ffmpeg.org/). This video source must support multiple simultaneous reads, because for every concurrent Home Assistant user, a connection will be made to the source every 10 seconds. Normally this should not be a problem.

## {% linkable_title Configuration %}

To enable your FFmpeg feed in your installation you must first configure the [ffmpeg component](/components/ffmpeg/), then add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
camera:
  - platform: ffmpeg
    input: FFMPEG_SUPPORTED_INPUT
```

{% configuration %}
input:
  description: An FFmpeg-compatible input file, stream, or feed.
  required: true
  type: string
name:
  description: Override the name of your camera.
  required: false
  type: string
extra_arguments:
  description: Extra options to pass to `ffmpeg`, e.g., image quality or video filter options.
  required: false
  type: string
  default: `-pred 1`
{% endconfiguration %}

### {% linkable_title Image quality %}

You can control the image quality with [`extra_arguments`](https://www.ffmpeg.org/ffmpeg-codecs.html#jpeg2000) `-q:v 2-32` or with lossless option `-pred 1`. Default is lossless.

If you are running into trouble with this sensor, please refer to the [Troubleshooting section](/components/ffmpeg/#troubleshooting).
