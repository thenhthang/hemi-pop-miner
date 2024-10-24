# Hemi Miner Incentivized Testnet

![image](https://github.com/user-attachments/assets/996c7d95-8be3-457b-a920-270fc337c6e1)
> Hemi is a modular protocol for superior scaling, security, and interoperability, powered by Bitcoin and Ethereum.
 
#
* You can run miner using web browser on windows here: https://pop-miner.hemi.xyz/
* Check point: https://testnet.popstats.hemi.network/
* Network status: https://hemistatus.com/

## Install Miner on Linux
**1. Download Binaries**
```bash
wget https://github.com/hemilabs/heminetwork/releases/download/v0.4.5/heminetwork_v0.4.5_linux_amd64.tar.gz
```

**2. Extract Binaries**
```bash
mkdir heminetwork && tar -xvf heminetwork_v0.4.5_linux_amd64.tar.gz -C heminetwork && rm heminetwork_v0.4.5_linux_amd64.tar.gz && cd heminetwork
```

## Wallet
**1. Create tBTC wallet**
```bash
./keygen -secp256k1 -json -net="testnet" > ~/popm-address.json
```

**2. Get tBTC address**
```bash
cat $HOME/popm-address.json
```
* Save the output
* `pubkey_hash` is your tBTC address

**3. Fund your wallet**
* Get tBTC faucet in [Discord](https://discord.gg/hemixyz) for your bitcoin wallet
* Check your txhash in explorer until it get CONFIRMED

## Start Miner
# Replace your private key with `PRIVATE_KEY`**
# create service
```
sudo tee /etc/systemd/system/hemid.service > /dev/null <<EOF
[Unit]
Description=Hemi network
After=network.target

[Service]
User=root
WorkingDirectory=$HOME/heminetwork
ExecStart=$HOME/heminetwork/popmd
Environment="POPM_BTC_PRIVKEY=PRIVATE_KEY"
Environment="POPM_STATIC_FEE=650"
Environment="POPM_BFG_URL=wss://testnet.rpc.hemi.network/v1/ws/public"
Restart=on-failure
RestartSec=10
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```
## Upgrade to last version v0.5.0
```
sudo systemctl stop hemid
cd heminetwork
wget https://github.com/hemilabs/heminetwork/releases/download/v0.5.0/heminetwork_v0.5.0_linux_amd64.tar.gz
tar -xzvf heminetwork_v0.5.0_linux_amd64.tar.gz
rm -rf heminetwork_v0.5.0_linux_amd64.tar.gz
sudo systemctl restart hemid
sudo journalctl -u hemid -f -o cat
```
# run
```
sudo systemctl daemon-reload && \
sudo systemctl enable hemid && \
sudo systemctl start hemid && \
sudo journalctl -u hemid -f -o cat
```
# log
```
sudo journalctl -u hemid -f -o cat
```
# stop miner
```
sudo systemctl stop hemid
```

# View your points
* Currently, the tHEMI token payout serves as Hemi PoP mining points. You will get tHEMI tokens for each block you min with your Hemi Pop Node
* To view your tHEMI balance, you may need to add the contract address `0x4200000000000000000000000000000000000042` as a "custom token" in your metamask wallet on Hemi Sepolia Network.
* You can also import your `private_key` here to check tHEMI balance: https://pop-miner.hemi.xyz/
* Gaining tHEMI is delayed rn, you can check later
