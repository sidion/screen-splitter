# screen-splitter
render a caputred monitor output over 2 screens

full writup to come just documenting command so i don't lose it

command used that was successful
ffplay -i /dev/video0 -f v4l2 -vf "crop=3840:1920:0:540" -noborder -alwaysontop -left 0 -top 0
