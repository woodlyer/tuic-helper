# tuic-helper
help you to run tuic.  based on https://github.com/EAimTY/tuic



tuic is a good proxy tool. location: https://github.com/EAimTY/tuic  
Doc at https://www.eaimty.com/2022/03/tuic.html . but not very enough.
This repository help you to run tuic.  

# quick tutorial

1.generate cert and key


2.edit the config_server.json


3.run tuic-server


4.edit the config_client.json



5.run tuic-client
```
.\tuic-client.exe  -c config_client.json 
```



# about tuic
Tuic is based on quic protocol.
Now it only support proxy mode.
It's developed with Rust.  

The speed of tuic is faster than hysteria and kcptun:  
tuic > hysteria > kcptun  



config.json from https://github.com/chika0801/tuic-install


# run tuic in the background.
run this command to create run.sh and run tuic-server in the background.
```
cat > run.sh << END

#!/bin/bash
nohup ./tuic-server -c config.json  > logtuic.log  2>&1 &
END

chmod +x run.sh
./run.sh
```















