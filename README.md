# Testnet-SUI-NODE-Wave2
<p align="center">
  <img height="150" height="auto" src="https://sui.io/_nuxt/img/sui-logo.8d3c44e.svg">
</p>

# SUI NODE - TESTNET (WAVE 2)

## 1. Ikhtisar

Testnet SUI Node (Wave 2) incentive ini khusus untuk orang yang telah mengikuti Testnet SUI Node di Wave 1 dan mendapatkan email dari Sui. Jika kalian tidak mendapatkan email atau tidak mengikuti di Wave 1, kalian tetap bisa menjalankan node nya, tetapi jangan berharap mendapatkan incentive ya...

## 2. Spesifiksi Rekomendasi

Berikut adalah persyaratan **rekomendari dari SUI** untuk menjalankan node SUI:

 -  **CPU** : 10 core
 -  **RAM** : Memori 16GB
 -  **HDD** : 1TB
 
Tapi saya mencoba ini di spek rendah dengan spesifikasi:
 -  **CPU** : 4 core
 -  **RAM** : Memori 8GB
 -  **HDD** : 400GB
 
# 1. Install Linux dependencies

```
sudo apt update \
&& apt-get install -y --no-install-recommends \
apt-transport-https \
ca-certificates \
curl \
software-properties-common
```

# 2. Install Docker

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt update \
sudo apt install docker-ce
```

# 3. Add your user to docker Group

```
sudo usermod -aG docker ${USER}
```

# 4. Install Docker Compose

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

# 5. Create SUI directory

```
mkdir -p $HOME/sui
cd $HOME/sui
```

# 6. Download fullnode.yaml

```
wget -O $HOME/sui/fullnode-template.yaml https://github.com/MystenLabs/sui/raw/main/crates/sui-config/data/fullnode-template.yaml
```

# 7. Download genesis state file

```
wget -O $HOME/sui/genesis.blob  https://github.com/MystenLabs/sui-genesis/raw/main/testnet/genesis.blob
```

# 8. Download docker-compose file and update Sui Node image in it

```
IMAGE="mysten/sui-node:2d07756360c28e35d7c60816bb0f1ed94ccf356e"
wget -O $HOME/sui/docker-compose.yaml https://raw.githubusercontent.com/MystenLabs/sui/main/docker/fullnode/docker-compose.yaml
sed -i.bak "s|image:.*|image: $IMAGE|" $HOME/sui/docker-compose.yaml
```

# 9. Start SUI Full Node in the Docker container

```
docker-compose up -d
```

# 10. Check logs from SUI Node container

```
docker ps
```
```
docker logs -f <container id>
```

## CTRL+C to exit logs

# Monitor your node health status
1. Go to https://www.scale3labs.com/check/sui
2. Insert your node ip
