# Stark & Wayne Videos

This site contains the metadata for each video episode of [Stark & Wayne Videos](https://www.starkandwayne.com/videos).

There is a Concourse CI pipeline to do much of the video processing and episode updating work (to YouTube and to the blog).

## Dimensions

Videos need to be 720p HD (16:9 aspect ratio) which is 1280x720 px. ScreenFlow can do cropping.

To continuously reuse the same 1280x720 region of your screen, perhaps use [LICEcap](http://www.cockos.com/licecap/) - not for its animated gif capturing features - rather just to set a box around a section of the screen. Set the capture area to 1280 x 720:

![licecap](http://cl.ly/1I3v1b2z052m/download/Image%202016-06-01%20at%2010.09.12%20AM.png)

Then position the windows being used into that space - iTerm, Chrome, etc. This will ensure that you can easily crop the video with ScreenFlow after recording.

## Exporting videos

We are publishing the videos to Vimeo. It provides recommendations https://vimeo.com/help/compression

Export to H.264 and set the bitrate to 5000 kbit/s.
