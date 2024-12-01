# ffclip

ffmpeg-based video cut & concat tool

基于ffmpeg的视频多剪一工具

## usage

ffclip [-I INPUTS ...] -O OUTPUT [clip-spec ...]

+ -I: input video, indexing from 0
+ -O: output video
+ clip-spec: [index@]start--end
	+ index: starting from this slice, switch to input video *index*, 0 if never specified
	+ start: start timestamp of the slice, [hh:]mm:ss[.ms]
	+ end: end timestamp of the slice, [hh:]mm:ss[.ms]

## notes

+ this is just a python script to generate ffmpeg *filter_complex* filter strings and then call ffmpeg to composite the video
+ seeking back in the same input video is known to cause ffmpeg to drain system memory and cause OOM
+ currently all input videos must have same resolution, working on this issue is planned
+ to reduce seeking time in input videos, it is recommended to corse-cut input videos using *-c:v copy -c:a copy* beforehand

## examples

```sh
ffmpeg -ss 1:40:00 -t 20:00 -i 1732880468.flv -c:v copy -c:a copy /tmp/1732880468.mp4
ffclip -I /tmp/1732880468.mp4 -I ~/Videos/elza_op.mp4 -I /tmp/1732880468.mp4 -O /tmp/1732880468_cut.mp4 0@7:51--8:12 1@00:00--00:07 2@3:08--6:10 2@7:40--18:10

```

## license

MIT License, Copyright (c) 2024 USN484259


