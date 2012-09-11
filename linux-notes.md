[title:Linux Notes]: /
[order:20]: /
[menu:Linux]: /

# Linux Notes  ###
List of common Linux things I've found useful.

## SSH  ###

If using a .pem file, don't forget to add to ssh. Use 'ssh-add {key}'

## Ports and processes  ###
ps aux to show all processes. ps f -p {id} to see details for a specific process id

port usage. lsof -i :8080 will show if something is using port. Can use process id to figure out exactly what it is. Also, netstat -lntp shows all listening ports with program name

## Terminal manager  ###
Started using Console2 on windows, and like having multiple command prompts in one window. dvtm is available for most linux systems, and provides similar functionality.

all commands start with ctrl-g

c=create
x=close
h/l=decrease/increase master size
j/k=focus next/previous window
.=minimize current window
u/i=focus next/prev non-min window
m=maximize current window
t=vertical stacking
g=grid layout
s=show/hide status bar
enter=zoom/cycle current window to/from master
space=toggle defined layouts
b=others on bottom
