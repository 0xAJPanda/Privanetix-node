# Privanetix Node Setup
# PrivaseaAI_Privanetix_Node

Technology that attests your human liveness to protect your digital presence from bots and AI impersonations.

**Raised : $15M**

Official Documentation : https://www.privasea.ai/privanetix-node

---

## Hardware requirements:

| **Hardware** | **Minimum Requirement** | **Reccomended** |
|--------------|-------------------------|-----------------|
| **CPU**      | 4 Cores                 | 16 cores        |
| **RAM**      | 4 GB                    | 8 GB 	         |
| **Disk**     | 100  GB  SSD            | 100 GB SSD	     |

---

### Update and Upgrade VPS

```
sudo apt update && sudo apt upgrade
sudo apt-get install ca-certificates curl
```

### Install Docker:

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg  
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null  
sudo apt-get update  
sudo apt-get install -y docker-ce docker-ce-cli containerd.io  
docker --version  
```
### Install Docker-Compose:

```
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)  
sudo curl -L "https://github.com/docker/compose/releases/download/$VER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose  
sudo chmod +x /usr/local/bin/docker-compose  
docker-compose --version  
```

### Docker Permission to User

```
sudo groupadd docker  
sudo usermod -aG docker $USER  
newgrp docker
```

### Pull Privasea docker Image

```
docker pull privasea/acceleration-node-beta:latest
```


### Create the program running directory and navigate to it:

```
mkdir -p  /privasea/config && cd  /privasea
```

### Create a new keystore file 

```
docker run -it -v "/privasea/config:/app/config" privasea/acceleration-node-beta:latest ./node-calc new_keystore
```

Note: The program will prompt you to enter a password, please remember this password for future use. The generated keystore file will have a corresponding node address, please save this address, it will be used in the dashboard configuration


**Example:**
```
Enter password for a new key:      # Enter wallet password  
Enter password again to verify:   # Re-enter the password for confirmation  
After successful creation of the wallet, the program will display information similar to the following:
```

**Sample:**
```
node address: 0xf07c3eF23ae7BEb8CD8bA5fF546E35Fd4b332B34
# This is the node address you generated, used for linking in the dashboard 
node filename: keystore:///app/config/UTC--2025-01-06T06-11-07.485797065Z--f07c3ef23ae7beb8cd8ba5ff546e35fd4b332b34

Instructions: 0xf07c3eF23ae7BEb8CD8bA5fF546E35Fd4b332B34 is an example and may differ in your case.
```

### Change to config directory 

```
cd /privasea/config && ls
```
### Rename the keystore file 

```
mv ./UTC--*  ./wallet_keystore 
```

### Link node address to reward address

- Visit : https://deepsea-beta.privasea.ai/privanetixNode

- Setup commission between 1 to 3 %


### Start the node

```
cd /privasea/ 
docker run  -d   -v "/privasea/config:/app/config" -e KEYSTORE_PASSWORD=123456 privasea/acceleration-node-beta:latest
```

**Replace with your password**

### Check Node Health

```
docker logs -f 
```

---

## Update node


### stop node

```
docker ps -q --filter "ancestor=privasea/acceleration-node-beta:latest" | xargs --no-run-if-empty docker stop
docker ps | grep privasea/acceleration-node-beta:latest
```

**Replace with your password**

```
cd /privasea/
docker run  -d   -v "/privasea/config:/app/config" -e KEYSTORE_PASSWORD=123456 privasea/acceleration-node-beta:latest
```


---

Follow : https://x.com/0xAJPanda

