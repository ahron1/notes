## ffmpeg

### Streamable files

To check if mp4 file is streamable:

    mediainfo -f file.mp4 | grep IsStreamable

To make mp4 streamable:

    ffmpeg -i INPUT -c copy -movflags faststart OUTPUT

### Cut section between timestamps

	ffmpeg -ss 00:01:00 -to 00:02:00 -i input.mp4 -c copy output.mp4

### Resize Video

#### Specify One Dimension

	ffmpeg -i input -filter:v scale=720:-1 -c:a copy output
	
#### Specify Both Dimensions

	ffmpeg -i input.avi -s 720x480 -c:a copy output.mkv

## Python

Install [qtfaststart](https://github.com/danielgtaylor/qtfaststart)
    
    pip install qtfaststart

Use `qtfaststart`. 

To overwrite the input file
    
    qtfaststart INPUT 


Create new output file

    qtfaststart INPUT OUTPUT


