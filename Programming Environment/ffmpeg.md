# ffmpeg

## Separate audio from video

- [stacks exchange](https://stackoverflow.com/questions/9913032/how-can-i-extract-audio-from-video-with-ffmpeg#), see also for extract within time range
`ffmpeg -i vid.mp4 -q:a 0 -map 0:a audio.m4a -map 0:v onlyvideo.mp4`
- 0: first input file
- -map: specifies which stream from which file to include in the output
- -q:a 0: selects the quality of the audio output to the highest 

## Convert audio format

`ffmpeg -i filename.opus -ab 320k -map_metadata 0:s:a:0 -id3v2_version 3 newfilename.mp3`
1. `ffmpeg`: This is the command to invoke FFmpeg.
2. `-i filename.opus`: This specifies the input file (`filename.opus`). FFmpeg uses this file as the source for processing.
3. `-ab 320k`: This sets the audio bitrate to 320 kbps for the output file. The `-ab` flag is used to specify the audio bitrate.
4. `-map_metadata 0:s:a:0`: This maps metadata from the input file to the output file. It ensures that metadata (like tags) from the first stream (`0:s:a:0`) is preserved. The `0:s:a:0` refers to the first audio stream of the input file.
5. `-id3v2_version 3`: This sets the ID3v2 version for the output MP3 file to version 3. ID3v2 is a metadata format used in MP3 files to store information such as artist, title, album, etc. Version 3 is specified here.
6. `newfilename.mp3`: This is the name of the output file. The processed audio will be saved as a new MP3 file with the specified name.

## Combine video and audio

`ffmpeg -i test.mp4 -i 哥谭噩梦原版视频.m4a -c:v copy -c:a aac swapped.mp4`

## Transcode video

`ffmpeg -i demo.mp4 -vcodec copy -acodec copy out.mp4`