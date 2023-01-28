## ffmpeg

To check if mp4 file is streamable:

    info -f file.mp4 | grep IsStreamable

To make mp4 streamable:

    ffmpeg -i INPUT -c copy -movflags faststart OUTPUT

## Python

Install
    
    pip install qtfaststart

Use `qtfaststart`. 

To overwrite the input file
    
    qtfaststart INPUT 


Create new output file

    qtfaststart INPUT OUTPUT
