# Multiple MasterNode

A script which is easily create Multiple Masternodes of the same coin in the same VPS.

First of all you have to start one masternode using <a href="https://github.com/LondiniumCryptoNew/Londinium-MN-Install#londinium-mn-install">install.sh</a> script that is your MainNode.

# Guide for Install MultiMN:

Install the multimn script 

`curl -sL https://raw.githubusercontent.com/LondiniumCryptoNew/Londinium-MultiMN-Script/master/multimn_install.sh | sudo -E bash -`

Add the coin profile.
```
wget -q https://raw.githubusercontent.com/LondiniumCryptoNew/Londinium-MultiMN-Script/master/profiles/londinium.mn
multimn profadd londinium.mn londinium
```
Now the Londinium profile is saved and the downloaded file can be removed if you want: `rm -rf londinium.dmn`

Stop the londinium Service:

`systemctl stop londinium`

Now create 3 extra instances (Ex. You want to make 3 Masternode):
```
multimn install londinium
multimn install londinium
multimn install londinium
```
You can check every MN like this:
```
londinium-cli-1 getinfo
londinium-cli-2 getinfo
londinium-cli-3 getinfo
londinium-cli-all getinfo
```
There's also a `londinium-cli-0`, that is a reference to the 'main node', not a created one with multimn.

Now, if you want to uninstall any instances,then just uninstall it with:

`multimn uninstall londinium 2` (Uninstall instance 2)

You can uninstall all of them with:

`multimn uninstall londinium all`


You can get priv key of all MN with:

`multimn list londinium --privkey`


Note this all priv key and make `masternode.conf` in your Coldwallet where you done MasternodeTx.
so `masternode.conf` look like this:
```
MN01 IP:9555 MN_PrivKey Tx_Hash Output_Index
MN02 IP:9555 MN_PrivKey Tx_Hash Output_Index
MN03 IP:9555 MN_PrivKey Tx_Hash Output_Index
MN04 IP:9555 MN_PrivKey Tx_Hash Output_Index
```

Here IP and port Same for all MN.

MN01 is your main_node MN which you create with <a href="https://github.com/LondiniumCryptoNew/Londinium-MN-Install#londinium-mn-install">install.sh</a> script.

MN02, MN03, MN04 is your masternode which you create with multimn.


Now StartMasternode from Coldwallet with:
```
startmasternode alias false MN01
startmasternode alias false MN02
startmasternode alias false MN03
startmasternode alias false MN04
```

Now StartMasternode in VPS with Service:

`systemctl start londinium` (Start your MN which is create with main_node <a href="https://github.com/LondiniumCryptoNew/Londinium-MN-Install#londinium-mn-install">install.sh</a> script)

Below 3 MN which is create with `multimn` script.
```
systemctl start   londinium-1.service
systemctl start   londinium-2.service
systemctl start   londinium-3.service
```

That's all now your MN start.





