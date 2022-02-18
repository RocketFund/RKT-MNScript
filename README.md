# Rocketfundcoin MN Setup (Ubuntu 16.04 / 18.04 / 20.04)
This guide will assist you in setting up a Rocketfundcoin Masternode on a Linux Server running Ubuntu 16.04 / 18.04 / 20.04

- [Rocketfundcoin Masternode Setup](#rocketfundcoin-masternode-setup)  
  	* [Requirements](#requirements) 
  * [Connecting to the VPS and installing the masternode script](#Connecting-to-the-VPS-and-installing-the-masternode-script)  
         [1. Log into the VPS with **root**](#1-log-into-the-vps-with-root)  
         [2. Git Installation](#2-git-installation)  
         [3. Clone MN setup script](#3-clone-mn-setup-script)  
         [4. Start MN setup script](#4-start-mn-setup-script)  
         [5. Copy Masternode Private Key](#5-copy-masternode-private-key-from-vps-console-window-and-pres-enter)
  * [Setup QT wallet](#setup-qt-wallet)  
         [1. Create new receiving address and copy it](#1-create-new-receiving-address-and-copy-it)  
	 [2. Send Collateral amount of Rocketfundcoin to copied address](#2-send-collateral-amount-of-rocketfundcoin-to-copied-address)  
	 [3. Get MN output and Set Masternode Configuration File](#3-open-console-get-mn-output-and-set-masternode-configuration-file-and-save-it)  
	 [4. Wait at least 15 confirmation of transaction](#4-wait-at-least-15-confirmation-of-transaction)  
         [5. Restart QT wallet](#5-restart-qt-wallet)  
         [6. Start MN in QT wallet console](#6-start-mn-in-qt-wallet-console)  
	 [7. Check Masternode Status in VPS](#7-check-masternode-status-in-vps)  

## Requirements
- MN Collateral amount of Rocketfundcoin.
- A VPS running Linux Ubuntu 16.04/18.04/20.04 with 1 CPU & 1GB Memory minimum (2gb Recommended) from [Vultr](https://www.vultr.com/?ref=8622028) or any other providers.
- Rocketfundcoin Wallet (Local Wallet)
- An SSH Client (<a href="https://www.putty.org/" target="_blank">Putty</a> or <a href="https://dl.bitvise.com/BvSshClient-Inst.exe" target="_blank">Bitvise</a>)


## Connecting to the VPS and installing the masternode script

##### 1. Log into the VPS with **root**  

##### 2. Git Installation:  
- ```sudo apt-get install -y git-core```  

##### 3. Clone MN setup script: 
- ```git clone https://github.com/RocketFund/RKT-MNScript.git```  

##### 4. Start MN setup script: 
##### For Ubuntu 16.04
- ```cd RKT-MNScript && chmod +x ./RKT-16.04-MN.sh && ./RKT-16.04-MN.sh```

##### For Ubuntu 18.04 & 20.04
- ```cd RKT-MNScript && chmod +x ./RKT-MN.sh && ./RKT-MN.sh```


   
**Now ask for VPS Public IP Address** 

**Now you need to wait some time, while script preparing the VPS to setup**  
##### 5. Copy masternode private key from VPS console window and pres "Enter":


- to check VPS daemon status, type: ```rocketfundcoin-cli getinfo```

**Don't close this window!** 	

## Setup QT wallet
##### 1. Create new receiving address and copy it

##### 2. Send Collateral amount of Rocketfundcoin to copied address

##### 3. Open console Get MN output and set masternode configuration file and save it
- ```mn1 VPS_IP:36145 masternode_genkey masternode_output output_index```:

##### 4. Wait at least 15 confirmation of transaction

##### 5. Restart QT wallet  
- **it's important**

##### 6. Start MN in QT wallet console:
- ```startmasternode alias false TEST-MN```

##### 7. Check Masternode Status in VPS:
- ```rocketfundcoin-cli startmasternode local false``` 
- ```rocketfundcoin-cli getmasternodestatus```  

**Сongratulations you did it!**



# Guide for Multiple MasterNode

A script which is easily create Multiple Masternodes of the same coin in the same VPS.



# Guide of use RKT-MN.sh for MainNode (Ubuntu 18.04 & 20.04):

First of all you have to start one masternode using <a href="https://github.com/RocketFund/RKT-MNScript/blob/main/RKT-MN.sh">RKT-MN.sh</a> script that is your MainNode.

```
wget -q https://raw.githubusercontent.com/RocketFund/RKT-MNScript/main/RKT-MN.sh
sudo chmod +x RKT-MN.sh
./RKT-MN.sh
```
***

# Guide of use RKT-16.04-MN.sh for MainNode (Ubuntu 16.04):

First of all you have to start one masternode using <a href="https://github.com/RocketFund/RKT-MNScript/blob/main/RKT-16.04-MN.sh">RKT-16.04-MN.sh</a> script that is your MainNode.

```
wget -q https://raw.githubusercontent.com/RocketFund/RKT-MNScript/main/RKT-16.04-MN.sh
sudo chmod +x RKT-16.04-MN.sh
./RKT-16.04-MN.sh
```
***


# Guide for Install MultiMN:

Install the multimn script 

`curl -sL https://raw.githubusercontent.com/RocketFund/RKT-MNScript/main/multimn_install.sh | sudo -E bash -`

Add the coin profile.
```
wget -q https://raw.githubusercontent.com/RocketFund/RKT-MNScript/main/profiles/rocketfundcoin.mn
multimn profadd rocketfundcoin.mn rocketfundcoin
```
Now the rocketfundcoin profile is saved and the downloaded file can be removed if you want: `rm -rf rocketfundcoin.dmn`

Stop the rocketfundcoin Service:
```
rocketfundcoin-cli stop
systemctl stop rocketfundcoin
```
Now create 3 extra instances with bootstrap (Ex. You want to make 3 Masternode):
```
multimn install rocketfundcoin --bootstrap
multimn install rocketfundcoin --bootstrap
multimn install rocketfundcoin --bootstrap
```
You can check every MN like this:
```
rocketfundcoin-cli-1 getinfo
rocketfundcoin-cli-2 getinfo
rocketfundcoin-cli-3 getinfo
rocketfundcoin-cli-all getinfo
```
There's also a `rocketfundcoin-cli-0`, that is a reference to the 'main node', not a created one with multimn.

Now, if you want to uninstall any instances,then just uninstall it with:

`multimn uninstall rocketfundcoin 2` (Uninstall instance 2)

You can uninstall all of them with:

`multimn uninstall rocketfundcoin all`


You can get priv key of all MN with:

`multimn list rocketfundcoin --privkey`


Note this all priv key and make `masternode.conf` in your Coldwallet where you done MasternodeTx.
so `masternode.conf` look like this:
```
MN0 IP:36145 MN_PrivKey Tx_Hash Output_Index
MN01 IP:36145 MN_PrivKey Tx_Hash Output_Index
MN02 IP:36145 MN_PrivKey Tx_Hash Output_Index
MN03 IP:36145 MN_PrivKey Tx_Hash Output_Index
```

Here IP and port Same for all MN.

MN0 is your main_node MN which you create with <a href="https://github.com/RocketFund/RKT-MNScript/blob/main/RKT-MN.sh">RKT-MN.sh</a> script.

MN01, MN02, MN03 is your masternode which you create with multimn.


Now StartMasternode from Coldwallet with:
```
startmasternode alias false MN0
startmasternode alias false MN01
startmasternode alias false MN02
startmasternode alias false MN03
```

Now StartMasternode in VPS with Service:

`systemctl start rocketfundcoin` (Start your MN which is create with main_node <a href="https://github.com/RocketFund/RKT-MNScript/blob/main/RKT-MN.sh">RKT-MN.sh</a> script)

Below 3 MN which is create with `multimn` script.
```
systemctl start   rocketfundcoin-1.service
systemctl start   rocketfundcoin-2.service
systemctl start   rocketfundcoin-3.service
```

That's all now your MN start.

