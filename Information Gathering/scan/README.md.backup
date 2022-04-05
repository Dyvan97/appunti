# Scanner

## bash

```
for PORT in {0..1000}; do timeout 1 bash -c "</dev/tcp/172.19.0.1/$PORT &>/dev/null"
2>/dev/null && echo "port $PORT is open"; done
```