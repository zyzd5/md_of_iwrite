```bash
#视频音频合并
ffmpeg -i ./video.mp4 -i ./audio.mp4 -vcodec copy -acodec copy output.mp4
#-i ./video.mp4：表示输入源为./video.mp4
#-vcode copy：使用视频流的拷贝（copy）方式，即不对视频进行重新编码，保持原有的编码方式
#-acode copy：使用音频流的拷贝方式，即不对音频进行重新编码，保持原有的编码方式。
#output.mp4: 指定输出文件的路径和名称为 output.mp4
```