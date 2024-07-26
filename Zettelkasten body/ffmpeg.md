что бы сделать видео быстрее
```bash
ffmpeg -i input.mkv -vf "setpts=0.2*PTS" -an output.mkv
```
