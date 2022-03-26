# Upgrade Shell

## script 

vittima:
```
SHELL=/bin/bash script -q /dev/null
Ctrl-Z
```

host:
```
stty raw -echo
fg
reset
xterm
```


## Python

richiede python3 installato (`python3 --version()`)

```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```



