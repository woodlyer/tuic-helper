# tuic-helper
tuic is a good proxy tool. location: https://github.com/EAimTY/tuic  
Doc locate at https://www.eaimty.com/2022/03/tuic.html , but it's not very clear.  
This repository helps you to run tuic.  

# download tuic  
Now the version is 0.8.5.
```
wget https://github.com/EAimTY/tuic/releases/download/0.8.5/tuic-server-0.8.5-x86_64-linux-gnu
wget https://github.com/EAimTY/tuic/releases/download/0.8.5/tuic-client-0.8.5-x86_64-linux-gnu
wget https://github.com/EAimTY/tuic/releases/download/0.8.5/tuic-client-0.8.5-x86_64-windows-gnu.exe
```


# quick tutorial

1. request [zerossl.com](https://zerossl.com/) or [letsencrypt.com](https://letsencrypt.org/) to generate cert and key

If you don't want to request a cert, just generate one, by yourself.  
In the cert dir, run ssl.sh to gnerate a cert and key.  
```
./ssl.sh  abc.com
```
It will produce serval files:
```bash
abc.com.crt  #certificate
abc.com.key  #private key

rootCA.crt   #ca cert
rootCA.key   #ca key 
```

2.edit the config_server.json
```
{
    "port": 16000,
    "token": ["chika"],
    "certificate": "./cert/abc.com.crt",
    "private_key": "./cert/abc.com.key",
    "ip": "::",
    "congestion_controller": "bbr",
    "alpn": ["h3"],
    "max_udp_relay_packet_size": 1146
}

```

3.run tuic-server
```
./tuic-server -c config_server.json
```

4.edit the config_client.json  
Iif you want to use domain ,keep the ip blank. 
```
{
    "relay": {
        "server": "abc.com",
        "port": 16000,
        "token": "chika",
        "ip": "10.0.0.1",
        "congestion_controller": "bbr",
        "alpn": ["h3"],
        "reduce_rtt": true,
        "max_udp_relay_packet_size": 1146,
        "certificates": ["cert/rootCA.crt"]
    },
    "local": {
        "port": 1080
    },
    "log_level": "info"
}
```


5.run tuic-client
```
# linux
.\tuic-client -c config_client.json  

# windows
.\tuic-client.exe  -c config_client.json  
```

# Windows GUI 
These terminal in windows will show a black window on the desktop.  
If you want to run the program in the background, please use [gostGUI](https://github.com/woodlyer/gostGUI).  
It's contained In this project.




# Run tuic in the background in Linux
use nohup to run tuic-server in the background.
```
nohup ./tuic-server -c config.json  > logtuic.log  2>&1 &
```


# About tuic
Tuic is based on quic protocol.
Now it only support proxy mode, doesn't support tunnel mode.
It's developed with Rust.  

The speed of tuic is faster than hysteria and kcptun:  
tuic > hysteria > kcptun  



# Reference
config.json from https://github.com/chika0801/tuic-install  
ssl.sh from https://devopscube.com/create-self-signed-certificates-openssl/

















