#SNiPhunter SNP search engine


##Local Machine (LM) installation

####After cloning this repository navigate to:

`/node_modules/json-server/bin`

####Now type:

`node index.js --watch JSONdbKeys.json`

or if you didn't create a symlink

`nodejs index.js --watch JSONdbKeys.json`

####Then open your browser and go to:

`http://localhost:3000`

##Virtual Machine (VM) installation

####SSH into the VM and run the following commands:

```sudo apt-get install nodejs
sudo ln -s `which nodejs` /usr/bin/node
sudo npm install -g forever-service
sudo npm install -g forever
sudo forever-service install sniphunter --script index.js -o " --watch JSONdbKeys.json"```

####To start the service type:

`sudo start sniphunter`

####To stop the service type:

`sudo stop sniphunter`

####Automated service on port 80 (Optional)

Open a crontab editor:

`sudo crontab -e`

Then enter the following in the crontab:

```0 0 * * * sudo reboot
@reboot sudo sysctl -w net.ipv4.ip_forward=1
@reboot sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 3000 
@reboot sudo start sniphunter```

####SNiPhunter LM and VM installations were tested on *Ubuntu v14.04*