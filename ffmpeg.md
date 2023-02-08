## ffmpeg

### Streamable files

To check if mp4 file is streamable:

    mediainfo -f file.mp4 | grep IsStreamable

To make mp4 streamable:

    ffmpeg -i INPUT -c copy -movflags faststart OUTPUT

### Cut section between timestamps

	ffmpeg -ss 00:01:00 -to 00:02:00 -i input.mp4 -c copy output.mp4
	
### Merge segments

Make file `mylist.txt` with list of clips:

	file '/path/to/file1'
	file '/path/to/file2'
	file '/path/to/file3'
	
Concat the files:

	 ffmpeg -f concat -safe 0 -i mylist.txt -c copy output.mp4

### Resize Video

#### Specify One Dimension

	ffmpeg -i input -filter:v scale=720:-1 -c:a copy output
	
#### Specify Both Dimensions

	ffmpeg -i input.avi -s 720x480 -c:a copy output.mkv
	
#### Adjust for scaling odd values

	ffmpeg -i input -filter:v scale="new_width:trunc(old_width/a/2)*2" -c:a copy output
	
	ffmpeg -i input -filter:v scale="trunc(old_height*a/2)*2:new_height" -c:a copy output
	
	ffmpeg -i input -filter:v scale=720:-2 -c:a copy output

Using -2 adjusts for odd values.

## Crop Video

	ffmpeg -i in.mp4 -filter:v "crop=w:h:x:y" out.mp4
	
w - width of cropped frame
h - height of cropped frame
x - origin X of cropped frame (wrt current frame)
x - origin Y of cropped frame (wrt current frame)

Frame's Origin is at top left corner.

### Preview Cropped Section

	ffplay -i input -vf "crop=....."

### Example

Crop 20 pixels from the top, and 20 from the bottom:	

	ffmpeg -i in.mp4 -filter:v "crop=in_w:in_h-40" -c:a copy out.mp4

## Padding

	 ffmpeg -i INPUT -vf "pad=width=640:height=480:x=0:y=120:color=black" OUTPUT
	 
Here the video output width and height are 640x480 and the image is placed 120 pixels from top, 0 pixels from left. 

## Python

Install [qtfaststart](https://github.com/danielgtaylor/qtfaststart)
    
    pip install qtfaststart

Use `qtfaststart`. 

To overwrite the input file
    
    qtfaststart INPUT 


Create new output file

    qtfaststart INPUT OUTPUT


