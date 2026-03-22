
This is a supporting repo for the blog post on https://blog.punit.in :

[Infinite Piano Stream: How I Built a Low-Cost, 100% AI-Generated YouTube Livestream](https://blog.punit.in/infinite-piano-stream-how-i-built-a-low-cost-100-ai-generated-youtube-livestream)

Only [FFMpeg](https://www.ffmpeg.org/download.html) is required.

Command to start a livestream with pre-generated assets:
(Replace the STREAM_KEY with the actual value)

```
ffmpeg -re \
    -f concat -safe 0 -stream_loop -1 -i assets/keyboard/video_list.txt \
    -f concat -safe 0 -stream_loop -1 -i assets/keyboard/audio_list.txt \
    -c:v libx264 -preset veryfast -b:v 4000k -maxrate 4000k -bufsize 8000k \
    -pix_fmt yuv420p -g 60 \
    -c:a aac -b:a 128k -ar 44100 \
    -map 0:v:0 -map 1:a:0 \
    -f flv "rtmp://a.rtmp.youtube.com/live2/STREAM_KEY"
```
