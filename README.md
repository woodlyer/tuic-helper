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

1.generate cert and key
Use ssl.sh to generate ssl certifacate.  
You don't need a real domain name.  
Just generate one.  
```
chmod +x ssl.sh
./ssl.sh abc.com
```
The script will create all the certificates and keys we created using the commands.  
The SSL certificate and private keys get named with the domain name you pass as the script argument.  
"abc.com.crt"  is cert file.  
"abc.com.key"  is private key file.  



2.edit the config_server.json
```
{
    "port": 16000,
    "token": ["chika"],
    "certificate": "/root/abc.com.crt",
    "private_key": "/root/abc.com.key",
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
        "max_udp_relay_packet_size": 1146
    },
    "local": {
        "port": 1080
    },
    "log_level": "info"
}
```


5.run tuic-client
```
.\tuic-client.exe  -c config_client.json 
```

# Windows GUI 
These terminal in windows will show a black window on the desktop.  
If you want to run the program in the background, please use gostGUI.  
https://github.com/woodlyer/gostGUI  



# Run tuic in the background in Linux
run this command to create run.sh and run tuic-server in the background.
```
cat > run.sh << END

#!/bin/bash
nohup ./tuic-server -c config.json  > logtuic.log  2>&1 &
END

chmod +x run.sh
./run.sh
```


# About tuic
Tuic is based on quic protocol.
Now it only support proxy mode.
It's developed with Rust.  

The speed of tuic is faster than hysteria and kcptun:  
tuic > hysteria > kcptun  



# Reference
config.json from https://github.com/chika0801/tuic-install  
ssl.sh from https://devopscube.com/create-self-signed-certificates-openssl/

















