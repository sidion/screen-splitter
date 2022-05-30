# screen-splitter
render a caputred monitor output over 2 screens

## Background:

I wanted to use 3 monitors with my work macbook, but it can only output 2 video outputs, 
2 of the monitors i wanted to use for this project are of a 1920x1080 resolution and the macbook can output a full 4k in both outputs


so the desire was to make the macbook think that the 2 1080 monitors are in fact 1 monitor and render accross both of them

----

### Step 1:

get a capture card, get an HDMI one because display port ones a STUPID expensive, you might need an active HDMI adapter to add a clock signal to the cable

*Note:* the capture card must capture at 4k, and give the computer a 4k render, many will capture in 4k for video passthrough but only provide a 1080p capture to the computer, i ended up using the elgato cam link as it could capture 3840x2160


### Step 2:

install `ffplay` on the computer that will be outputing onto the 2 monitors


### Step 3:

plug in computer and set second monotor output to a 3840x1080 resolution


### Step 4:

do the thing:


`ffplay -i /dev/video0 -f v4l2 -vf "crop=3840:1920:0:540" -noborder -alwaysontop -left 0 -top 0`


**breakdown:**

`ffplay` : just the name of the command as opposed to ffmpeg 


`-i /dev/video0` : input source this is assumeing you only have 1 video input if you also have webcams or something it might be a different number


`-f v4l2` : i was doing this on a rasberry pi so was using the https://en.wikipedia.org/wiki/Video4Linux codex


`-vf "crop=3840:1080:1920:540"` : because the camlink captures a 3840x2160 resolution we need to crop down to the actual rendered screen


`-no border -alwaysontop` : cover regular UI elements and hide all UI of the ffplay window


`-left 0 -top 0` : start drawing the ffplay window at the top right of the screen so that it fully fills both monitors



----

*Note:* i was using a rasberry pi and overheated and killed the chip durring this process, if you are going to use a pi make sure it is actively cooled but i'm not sure if its powerful enough to handle a good enough refresh rate to really use smoothly as a 2nd and 3rd monitor so i might need a more powerful intermediary comupter
