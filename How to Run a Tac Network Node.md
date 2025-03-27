# ⚙️How to run a Tac Network Node⚙️

![image](https://github.com/user-attachments/assets/7fc134aa-15ed-42c6-b190-67848b4ce9f9)

---

## Step 1 : Setting up a VPS
You can choose CLOUP VPS 2 on Contabo : https://www.tkqlhce.com/click-101114590-13484397

![image](https://github.com/user-attachments/assets/94b0b6f0-5f38-46a0-a3c7-93de207a4ac9)

- Select Ubuntu 22.04


## Step 2: Connect to your VPS
 ```
ssh root@<IP_OF_YOUR_VPS>
 ```
## Step 3: Configure your node

- Update your system
 ```
sudo apt update && sudo apt upgrade -y
 ```
- Install Go
 ```
curl -OL https://go.dev/dl/go1.21.0.linux-amd64.tar.gz
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf go1.21.0.linux-amd64.tar.gz
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc
 ```
- Install screen
 ```
apt install screen
 ```
- Check Go version
 ```
go version
 ```
- Install jq
 ```
sudo apt install -y jq
 ```
- Install curl
 ```
sudo apt install -y curl
 ```
- Check curl version
 ```
curl --version
 ```
- Install tacchaind
 ```
git clone https://github.com/TacBuild/tacchain
cd tacchain
make install
 ```
- Initialize Your Node
 ```
tacchaind init testnode --chain-id tacchain_2390-1 --home .testnet
 ```
- Edit your .testnet/config/config.toml
 ```
nano .testnet/config/config.toml
 ```
- Modify the Moniker name(write the node name)

- Copy this content on this file
 ```
# Set block time
timeout_commit = "3s"

# Add persistent peers
persistent_peers = "9b4995a048f930776ee5b799f201e9b00727ffcc@107.6.94.246:45120,e3c2479a6f418841bd64bae6dff027ea3efc1987@72.251.230.233:45120,fbf04b3d67705ed48831aa80ebe733775e672d1a@107.6.94.246:45110,5a6f0e342ea66cb769194c81141ffbff7417fbcd@72.251.230.233:45110"
 ```
- Save the file with CTRL+X write Y press Enter
- Download Genesis File
 ```
curl https://newyork-inap-72-251-230-233.ankr.com/tac_tacd_testnet_full_tendermint_rpc_1/genesis | jq '.result.genesis' > .testnet/config/genesis.json
 ```
- Create a new screen session
 ```
screen -S Tac
 ```
- Start Your Node
 ```
tacchaind start --chain-id tacchain_2390-1 --home .testnet
 ```
- Leave the screen
CTRL+A+D

- If you want to check the logs attach to the screen again
 ```
screen -r Tac
 ```
- Don’t forget to leave the screen session before exiting

CTRL+A+D

---

Thank’s for reading
If you need help you can join Discord : https://discord.com/invite/szXyZSgSYg
Twitter : https://x.com/TRTtheSalad
Disclaimer : Not a financial Advice an education tutorial do your own research
