# Masternode Setup - Step by step guide
Requirements: 	
1.) VPS for example on vultr or AWS on Amazon Services or Digital Ocean (on digitalocean you can get bonus 50$ for 30 days)
2.) for 1 Masternode you need a wallet with 10001 OZTG Coins
Feel free to use our reflinks to signup: 
vultr:  <a href="https://www.vultr.com/?ref=7811287"><img src="https://www.vultr.com/media/banner_2.png" width="468" height="60"></a>
Feel free to use our reflinks to signup: 
DigitalOcean ( to get the Bonus of 50$ ) you can use this link: https://m.do.co/c/620c3ac29a40
 
## start in the wallet 
in wallet: Open Debug console: 

```bash
masternode genkey
```
<table>
<tr><td>example</td></tr>
<tr><td>7ehsxiEwmLzeT4EaCuX9v2euuYQNGSjjBKxRUTrmbdXG</td></tr>
</table>

```bash
getaccountaddress "MN1"  
```
<table>
<tr><td>example</td></tr>
<tr><td>xfdbcQmmJUUPJ9RKZfa1ariykE1z774156P</td></tr>
</table>

send exact 10000 Coins to the address (confirmation need: 15) 


# Installation: for Security use SSH on your vps!!
setup start with security on vps in putty (firewall)
```bash
sudo ufw allow 22
```
```bash
sudo ufw allow 80
```
```bash
sudo ufw allow 8386
```
```bash
sudo ufw enable
```
You will be prompted with "Yes or no". type y and press enter
```bash
sudo ufw default deny
```
start install the requirements on VPS:
```bash
sudo apt-get update
```
```bash
sudo apt-get upgrade -y
```
```bash
sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils python3 libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboost-test-dev libboost-thread-dev libboost-all-dev libboost-program-options-dev -y
```
```bash
sudo apt-get install libminiupnpc-dev libzmq3-dev libprotobuf-dev protobuf-compiler unzip software-properties-common -y
```
```bash
sudo add-apt-repository ppa:bitcoin/bitcoin
```
You will be prompted with "Enter". press enter
```bash
sudo apt-get update
```
add another user for security reason!:
```bash
sudo adduser yourusername
```
You will be prompted with Set a password. type a good password and press enter
again You will be prompted with rename the password. type your password and press enter
you will be prompted for some account details: press 5 times enter 
You will be prompted with "Yes or no". type y and press enter
```bash
sudo usermod -aG sudo yourusername
```
change to user 
```bash
su - yourusername
```
download the wallet-client, tx and daemon file
```bash
sudo wget https://github.com/coindevelopments/oztg/raw/master/Linux/ozeety-cli
```
fillout the password of your username and press enter
```bash
sudo wget https://github.com/coindevelopments/oztg/raw/master/Linux/ozeety-tx
```
```bash
sudo wget https://github.com/coindevelopments/oztg/raw/master/Linux/ozeetyd
```

```bash
sudo chmod +x ozeetyd
```
```bash
sudo chmod +x ozeety-tx
```
```bash
sudo chmod +x ozeety-cli
```
```bash
sudo mv ozeetyd ozeety-cli ozeety-tx /usr/bin/
```
```bash
sudo apt-get install libdb4.8-dev libdb4.8++-dev -y
```
```bash
mkdir $HOME/.ozeety
```
```bash
nano $HOME/.ozeety/ozeety.conf
```
copy this with your details in th conf. file (choose only another good password, you need your masternode genkey from wallet and the ip address of the vps server)
```bash
#----
rpcuser=rpc_ozeety
rpcpassword=chooseagoodpassword
rpcallowip=127.0.0.1
#----
listen=1
server=1
daemon=1
maxconnections=64
#----
masternode=1
masternodeprivkey=your-MASTERNODE-GENKEY-from-debugconsole
externalip=IP-address
addnode=167.71.133.98 
addnode=159.65.60.210 
addnode=167.71.66.94 
addnode=167.71.72.227 
addnode=167.71.70.187
addnode=35.177.50.151
addnode=13.234.231.95
addnode=15.164.221.49
addnode=13.229.230.32
addnode=54.79.95.156
addnode=3.112.46.211
addnode=35.183.183.6
addnode=18.130.215.79
addnode=13.53.169.94
addnode=18.229.123.77
addnode=3.8.177.5
addnode=165.22.220.112 
addnode=165.22.220.120 
addnode=165.22.220.118 
addnode=134.209.203.102 
addnode=167.71.67.96 
addnode=165.22.213.1 
addnode=134.209.109.41
addnode=159.65.190.153
addnode=68.183.11.226
#----
```
save this file by pressing CONTROL+O and press enter
close this file by pressing CONTROL+X
# start the vps server with
```bash
ozeetyd
```
if everything is fine: you get an output: ozeety server starting



### back in wallet
 
go to debug console
```bash
masternode outputs
```
<table>
<tr><td>example</td></tr>
 <tr><td>{</td></tr>
<tr><td>    "txhash": "c8ab8aa43d50cae6bf2b89b09f124bd83beaec00537884be8ec6585d1922", </td></tr>
<tr><td>     "outputidx": 1 {</td></tr>
<tr><td>   }</td></tr>
</table>
# Configure masternode.conf file (look at the example in file), reopen wallet and start masternode in debug console
<table>
<tr><td>example for masternode in masternode.conf file </td></tr>
<tr><td>mn1 IP_OF_THE_SERVER:8386 MASTERNODE_GENKEY TX_HASH TX_OUTPUTS</td></tr>
<tr><td>mn1 123.12.15.14:8386 6ehsxiEwmLzeT4EaCuX9v2euuYQNGSjjBKxRUTrmbdXG c8ab8aa43d50cae6bf2b89b09f124bd83beaec00537884be8bae6585d1922 1</td></tr>
</table>

save file, reopen wallet and start in debug console !

```bash
startmasternode alias false MN1
```
