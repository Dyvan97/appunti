# Upgrade Shell

## script 

vittima:
```
SHELL=/bin/bash script -q /dev/null
Ctrl-Z
echo $TERM
stty -a
```

host:
```
stty raw -echo
fg
reset
xterm
stty rows <row> columns <column> 
```


## Python

richiede python3 installato (`python3 --version()`)

```
python3 -c 'import pty;pty.spawn("/bin/bash")'
```



