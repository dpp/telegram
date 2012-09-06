[title:Linux Notes]:
[date:2012-08-24]:

List of common Linux things I've found useful.

## SSH

If using a .pem file, don't forget to add to ssh. Use 'ssh-add {key}'

## Ports and processes
ps aux to show all processes. ps f -p {id} to see details for a specific process id

port usage. lsof -i :8080 will show if something is using port. Can use process id to figure out exactly what it is. Also, netstat -lntp shows all listening ports with program name
