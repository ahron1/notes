To check if mp4 file is streamable:

    info -f file.mp4 | grep IsStreamable

To make mp4 streamable:

    ffmpeg -i INPUT -c copy -movflags faststart OUTPUT


