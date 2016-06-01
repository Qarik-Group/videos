# Stark & Wayne Videos

This site contains the metadata for each video episode of [Stark & Wayne Videos](https://www.starkandwayne.com/videos).

There is a Concourse CI pipeline to do much of the video processing and episode updating work (to YouTube and to the blog).

## Producing videos

### Consistent tools

It is important that the videos are consistent - regardless of presenter. We can't fix presenters' accents... or can we? But we can at least use a consistent set of tools on screen:

* [iTerm2](https://www.iterm2.com/) (v3.0.0+)
* [Atom](https://atom.io/)
* [Chrome](https://www.google.com/chrome/)

Why use these tools for new videos? They were the tools used in the original videos.

### Terminal settings

```
export PS1="%~%% "
```

If you use oh-my-zsh, then reset to no theme. Replace `$ZSH_THEME` in `~/.zshrc` with `""`:

```
ZSH_THEME=""
```

The root working folder is to be called `~/workspace`. For example, if you are working inside the concourse-tutorial project, then that repo would be cloned into `~/workspace` as `~/workspace/concourse-tutorial`.

The iTerm2 prompt would look like:

```
~/workspace/concourse-tutorial%
```

Set the font to 15pt Monaco:

![iterm2](http://cl.ly/0n3K1p0c0f0e/download/Image%202016-06-01%20at%2010.50.14%20AM.png)

```
/usr/libexec/PlistBuddy -c "Set :\"New Bookmarks\":0:\"Normal Font\" \"Monaco 15\""  ~/Library/Preferences/com.googlecode.iterm2.plist
```

Set the New Window size to 141 x 33. This nicely fits into 1280x720px.

```
/usr/libexec/PlistBuddy -c "Set :\"New Bookmarks\":0:\"Columns\" 141"  ~/Library/Preferences/com.googlecode.iterm2.plist
/usr/libexec/PlistBuddy -c "Set :\"New Bookmarks\":0:\"Rows\" 33"  ~/Library/Preferences/com.googlecode.iterm2.plist
```

### Dimensions

Videos need to be 720p HD (16:9 aspect ratio) which is 1280x720 px. ScreenFlow can do cropping.

To continuously reuse the same 1280x720 region of your screen, perhaps use [LICEcap](http://www.cockos.com/licecap/) - not for its animated gif capturing features - rather just to set a box around a section of the screen. Set the capture area to 1280 x 720:

![licecap](http://cl.ly/1I3v1b2z052m/download/Image%202016-06-01%20at%2010.09.12%20AM.png)

Then position the windows being used into that space - iTerm, Chrome, etc. This will ensure that you can easily crop the video with ScreenFlow after recording.

### Exporting videos

We are publishing the videos to Vimeo. It provides recommendations https://vimeo.com/help/compression

Export to H.264 and set the bitrate to 5000 kbit/s.
