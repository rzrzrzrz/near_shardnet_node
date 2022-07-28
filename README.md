## Near shardnet node

<p align="center">
   Stake Wars: Episode III. Near shardnet node setup guide
</p>

* More info on Stake Wars: https://near.org/stakewars/
* What is a Chunk only Producer: https://near.org/decentralize/
* Registration form: https://nearprotocol1001.typeform.com/to/Z39N7cU9

<br></br>

<p align="center">
  <b> Challenge I-IV </b>
</p>


 * To create a NEAR test wallet visit https://wallet.shardnet.near.org/ 

<p>
  <img width="400" src="https://user-images.githubusercontent.com/104324209/181293718-46f27c1a-92dd-452c-bf64-97e8f82ff706.png" alt="Near">
</p>

 * Press "Create account". Enter desired username, make sure it's available.

<p>
  <img width="400" src="https://user-images.githubusercontent.com/104324209/181294726-e0f7f4a3-fc44-48d4-9e2d-69e170fba001.png">
</p>

 * Choose Security Method. Secure Passphrase is preferrable. 
 
<p>
  <img width="400" src="https://user-images.githubusercontent.com/104324209/181295461-79e7a788-ed3b-4dc3-aa05-0b48a7217b94.png">
</p>

 * Save your passphrase

 * Reenter it to recover wallet

<p>
  <img width="400" src="https://user-images.githubusercontent.com/104324209/181296983-f1faebc7-5920-481a-9115-6d2f2bcac45b.png">
</p>

 * Now your wallet balance should have some Near tokens

<p>
  <img width="400" src="https://user-images.githubusercontent.com/104324209/181297312-403f025e-61a1-4161-ad54-f55a5ab15db4.png">
</p>

* Choose your cloud server provider. Bear in mind the specs:
  CPU: 4-Core CPU with AVX support
  RAM: 8 GB DDR4
  Storage: 500GD SSD
  - Amazon Web Services
  - Google Cloud Platform
  - Microsoft Azure
  - IBM Cloud
  - DigitalOcean
  - Hetzner
    
* Let's choose Contabo https://contabo.com/  It will cost you around $11.39/month if you choose EU location using UBUNTU 20.04.

<p>
  <img width="600" src="https://user-images.githubusercontent.com/104324209/181313337-08c0a83b-7e30-477a-8cda-993278c7d676.png">
</p>

* Check to confirm that your machine has the right CPU features:

<code>
lscpu | grep -P '(?=.*avx )(?=.*sse4.2 )(?=.*cx16 )(?=.*popcnt )' > /dev/null \
&& echo "Supported" \
|| echo "Not supported"
</code>
  <br></br>
  Result:
  
  <blockquote>
  Supported
  </blockquote>
  
  
* Update your server

<code>
sudo apt update && sudo apt upgrade -y
</code>
<br></br>

* Install node.js and npm
<code>
curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -  
sudo apt install build-essential nodejs
PATH="$PATH"
</code>
<br></br>

* Check versions
<code>
 node -v
</code>
<br></br>
Result:
  <blockquote>
  v18.xx
  </blockquote>
<br></br>
<code>
npm -v
</code>
<br></br>
Result:
  <blockquote>
  8.xx
  </blockquote>
<br></br>

* Install Near-CLI
<code>
sudo npm install -g near-cli
</code>
<br></br>

  * Environment setup
<code>
export NEAR_ENV=shardnet
  
echo 'export NEAR_ENV=shardnet' >> ~/.bashrc</code>
<br></br>

  * Install developer tools

<code>
  sudo apt install -y git binutils-dev libcurl4-openssl-dev zlib1g-dev libdw-dev libiberty-dev cmake gcc g++ python docker.io protobuf-compiler libssl-dev pkg-config clang llvm cargo
  </code>
<br></br>  

  * Install Python pip

<code>
  sudo apt install python3-pip
  </code>
 <br></br>
 
  * Setup configuration

<code>
USER_BASE_BIN=$(python3 -m site --user-base)/bin
  
export PATH="$USER_BASE_BIN:$PATH"  </code>
 <br></br>
 
 * Install Clang, Rust & Cargo. Press "1" on installation options. 
<code>
sudo apt install clang build-essential make
  
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
  
source $HOME/.cargo/env
</code>
 <br></br>
  
* Clone nearcore repository

<code>
  git clone https://github.com/near/nearcore 
  
cd nearcore   
git fetch
  </code>
 <br></br>
 
 * Change "commit" to this value: https://github.com/near/stakewars-iii/blob/main/commit.md
  
  <code>
    git checkout commit
    </code>
  <br></br>
  
  * Build binary
  
  <code>
    cargo build -p neard --release --features shardnet
  </code>
   <br></br>
  
  * Create working directory and config files
  
  <code>
   ./target/release/neard --home ~/.near init --chain-id shardnet --download-genesis
  </code>
   <br></br>
  
  * Config.json
  
   <code>
  rm ~/.near/config.json
  
wget -O ~/.near/config.json https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/config.json
  </code>
   <br></br>
   
  * Install AWS CLI

  <code>
sudo apt-get install awscli -y
  </code>
   <br></br>
   
   * Genesis.json
  
   <code>
  rm ~/.near/genesis.json
  
cd ~/.near
wget https://s3-us-west-1.amazonaws.com/build.nearprotocol.com/nearcore-deploy/shardnet/genesis.json
  </code>
   <br></br>
   
  * Activate your node as validator

<code>
  near login
</code>
 <br></br>
   
  * Copy the link and paste it into the browser. It could look like that: https://wallet.shardnet.near.org/login/?referrer=NEAR+CLI&public_key=ed25519%3AGdA9fDgq2EngbxzKjzszxpQ9V6xMxqx9qjeZeiMYvoQC&success_url=http%3A%2F%2F127.0.0.1%3A5000

* Connect with NEAR and give full access to the app. Sign the approval with your wallet name. It should look like that: <your_name>.shardnet.near

<p>
  <img width="400" src="https://user-images.githubusercontent.com/104324209/181525534-0812b62d-93f9-4eff-aff4-d33ae6439f3a.png">
</p>

* You will get error message with 127.0.0.1 connection refusal. That is ok, return to the terminal of your server. 
* Type in your wallet address as shown, just change *yourname* to actual name of your wallet, press "Enter".

  <p>
  <img width="400" src="https://user-images.githubusercontent.com/104324209/181545257-882789d8-905f-4720-b2ce-9c6a04b1088c.png">
</p>

  * Create validator_key.json. pool_id should be yourname.factory.shardnet.near. Replace *yourname* with your wallet name.
  
  <code>
  near generate-key pool_id
</code>
  <br></br>
  
  * Copy this file to *shardnet* folder. Replace *yourwallet* with your wallet name. 
  
   <code>
  cp ~/.near-credentials/shardnet/yourwallet.json ~/.near/validator_key.json
</code>
  <br></br>
  
  * Now it's time for validator_key.json
  
<code>
    nano ~/.near/validator_key.json
</code>
  <br></br>
   
  * Change "account_id" to yourname.factory.shardnet.near, where <yourname> is actual name of your wallet. Change "private_key" to "secret_key". Save changes with *Ctrl+S*. Exit redactor with *Ctrl+X*.
  
<code>
 {
  "account_id": "yourname.factory.shardnet.near",
  "public_key": "ed25519:*************************************",
  "secret_key": "ed25519:*************************************"
}
</code>
  <br></br>
  
  * Create service file
 
<code>
 sudo nano /etc/systemd/system/neard.service
</code>
  <br></br>
  
  * Paste the following code. Change *USER* to your wallet name (f.e. *john*) in User, WorkingDirectory and ExecStart lines. Save changes and exit redactor.

<code>
 [Unit]
Description=NEARd Daemon Service

[Service]
Type=simple
User=USER
#Group=near
WorkingDirectory=/home/USER/.near
ExecStart=/home/USER/nearcore/target/release/neard run
Restart=on-failure
RestartSec=30
KillSignal=SIGINT
TimeoutStopSec=45
KillMode=mixed
[Install]
WantedBy=multi-user.target
</code>
  <br></br>
  
  * Run validator node

<code>
 sudo systemctl daemon-reload
sudo systemctl enable neard
sudo systemctl start neard
</code>
  <br></br>
  
  * Create logs and wait for full sync. It could take up to 20 minutes depending on your actual machine.

<code>
sudo apt install ccze
  
journalctl -n 100 -f -u neard | ccze -A
</code>
  <br></br>

* Run staking pool. Change *pool id* to your wallet name (f.e. *john*), *owner_id* to shardnet account name (f.e. *john.shardnet.near*), *public key* to public key from validator_key.json, *accounID* to shardnet account name (f.e. *john.shardnet.near*). Change pool fee to whatever you like, it's at 5% now. You can find it besides the numerator, number 5.

<code>
near call factory.shardnet.near create_staking_pool '{"staking_pool_id": "pool id", "owner_id": "accountId", "stake_public_key": "public key", "reward_fee_fraction": {"numerator": 5, "denominator": 100}, "code_hash":"Xxxxxxx88x8x8x8x8x8x8xxxxx99xxxxX"}' --accountId="accountId" --amount=450 --gas=300000000000000
</code>
  <br></br>
  
  * You can find your pool here: https://explorer.shardnet.near.org/nodes/validators It may not work straight away.

* Create task for autoping

<code>
cd
mkdir scripts
cd scripts
nano ping.sh
</code>
  <br></br>
  
  * Insert text. Change *USER*, *YOUR_POOL_ID*, *YOUR_ACCOUNT_ID* to your name. Most probably it will all be the same (f.e. *john*). 

<code>
#!/bin/sh
# Ping call to renew Proposal added to crontab
export NEAR_ENV=shardnet
export LOGS=/home/USER/logs
export POOLID=YOUR_POOL_ID
export ACCOUNTID=YOUR_ACCOUNT_ID
echo "---" >> $LOGS/all.log
date >> $LOGS/all.log
near call $POOLID.factory.shardnet.near ping '{}' --accountId $ACCOUNTID.shardnet.near --gas=300000000000000 >> $LOGS/all.log
near proposals | grep $POOLID >> $LOGS/all.log
near validators current | grep $POOLID >> $LOGS/all.log
near validators next | grep $POOLID >> $LOGS/all.log
  </code>
 <br></br> 
  
  * Create new crontab task

<code>
crontab -e
  </code>
 <br></br> 
  
  * Change script file using your *USER*, save and exit.

<code>
*/5 * * * * sh /home/USER/scripts/ping.sh
  </code>
 <br></br> 
 
 * Check if it's working

<code>
crontab -l
  </code>
 <br></br>
 
 * Check your logs, don't forget to change *USER* beforehand

<code>
cat home/USER/logs/all.log
  </code>
 <br></br>
 
 
