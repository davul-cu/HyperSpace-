# HyperSpaceAI 
## We will install this project in CLI . First of all, we can go to website and get the publıc and private keys.Please click key button image and to copy private key.Don't fotrget to save the key!. 
Go to the Website: https://node.hyper.space/
![Ekran görüntüsü 2025-01-06 174346](https://github.com/user-attachments/assets/e6169fa6-77f3-4db3-a19e-15185c80b4ca) 
![Ekran görüntüsü 2025-01-06 181256](https://github.com/user-attachments/assets/c37f91a9-df35-47e4-9aa8-f4fdbddf518e)

### Install and Update the server 
```
apt update && apt upgrade -y
apt install -y curl wget
```

```
curl https://download.hyper.space/api/install | bash
source ~/.bashrc
```

## Proof the CLI is working, version should be 0.1.6

```
aios-cli version
```

## Create a Systemd Service File For CLI 
```
nano /etc/systemd/system/aios.service
```

## Add the configuration file and paste the following section into this field. Exit the file by pressing ctrl+x+y
```
[Unit]
Description=aiOS CLI Service
After=network.target

[Service]
ExecStart=/root/.aios/aios-cli start
Restart=always
RestartSec=5
User=root
WorkingDirectory=/root
Environment=PATH=/usr/local/bin:/usr/bin:/bin:/root/.aios

[Install]
WantedBy=multi-user.target
```


## Now, Activate the Service
```
sudo systemctl daemon-reload

sudo systemctl start aios.service

sudo systemctl enable aios.service

sudo systemctl status aios.service
```
# Logs are seen like this. 
![Ekran görüntüsü 2025-01-08 165220](https://github.com/user-attachments/assets/472013de-3b0c-41f2-b483-210e6ad69f65)

## Now,Let's get our private key that we copied and saved

```
echo "YOUR PRIVATE KEY" > my-key.base58
```
```
/root/.aios/aios-cli hive import-keys ./my-key.base58
```
## Let's Sign in
```
aios-cli hive login
```
## Check Session Status
```
aios-cli hive whoami
```
- You will see the your public and private key

## Now, Tier Selection
-If you select tier 3 you will receive 2x points.(minimum CPU should be 6 or 8)
```
aios-cli hive select-tier 5
```
## Download Model 
```
aios-cli models add hf:TheBloke/phi-2-GGUF:phi-2.Q4_K_M.gguf
```

## Connect to Hive Network.In here, you can wait for a while.Let's contunie after the response.
```
aios-cli hive connect
```
## Check your connection status and points

```
aios-cli hive points
```
![Ekran görüntüsü 2025-01-08 170428](https://github.com/user-attachments/assets/8920e05c-649d-4b7a-b704-df58262f346f)

## Check the logs

```
journalctl -u aios.service -xe
```
## Useful Commands
```
aios-cli hive disconnect
```
```
aios-cli hive connect
```
```
#Delete service
systemctl stop aios.service
systemctl disable aios.service
rm /etc/systemd/system/aios.service
systemctl daemon-reload
#Delete Binary files
rm /usr/local/bin/aios-cli
```



