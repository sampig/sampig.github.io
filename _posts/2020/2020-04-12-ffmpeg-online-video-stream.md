---
layout: post
title: "Using ffmpeg for Online Video Stream"
date: 2020-04-12 12:45:00 +0200
category: tutorial
tagline: ""
tags: [Linux, Video]
abstract : "Learning ffmpeg for online video stream. This is just a note for myself."
---
{% include JB/setup %}

* [Introduction](#introduction)
* [Usage for Online Video Stream](#usage-for-online-video-stream)
* [Summary](#summary)
* [References](#references)


# Introduction

FFmpeg is a free and open-source project consisting of a vast software suite of libraries and programs for handling video, audio, and other multimedia files and streams. It can be used to record, convert and stream audio and video.


# Usage for Online Video Stream

Command:
```
ffmpeg -i "URL_FOR_m3u8_FILE" -bsf:a aac_adtstoasc -vcodec copy -c copy -crf 50 LOCAL_FILENAME.mp4
```

Explanation:
```
-bsf:a aac_adtstoasc
    bsf = (bit stream filter)
    use aac_adtstoasc bsf for a audio streams, this is need if .m3u8 file consists with .ts files and output is .mp4
    reference https://ffmpeg.org/ffmpeg-bitstream-filters.html#aac_005fadtstoasc

-c copy -vcodec copy
    skip codec (encode and decode), for demuxing and muxing
    for video stream, using H.264 codec.
    reference https://ffmpeg.org/ffmpeg.html#Stream-copy

-crf 50
    0 is lossless, 23 is the default, and 51 is worst quality
    reference https://trac.ffmpeg.org/wiki/Encode/H.264#CRFExample
```


# Summary

This is just a note for myself. If you want to know more about this tool, search it on its official website. I bet you will like it.


# References

1. [FFmpeg.org](http://ffmpeg.org/){:target="_blank"}
