# autominer
automated bittensor mining

Recommended to setup a ssh config. This will make transferring keys and file easier later on:

```
cd ~/.ssh
```
```
vim config
```	

```	
Host <>
	HostName <IP>
	Port <>
	User <>

Host <>
	HostName <IP>
	Port <>
	User <>

Host <>
	HostName <IP>
	Port <>
	User <>
```

Step 1:

	git clone [https://github.com/quac88/autominer/tree/main](https://github.com/quac88/autominer/tree/main)

Step 2:

	Open the directory:

		cd autominer
		

Step 2: 

	Configure the yaml:

	Each “-” represents a GPU
	
		machine1:
		  -
		    name: "a"
		    model: "gpt2"
		    port: 8091
		    keyfile: 0
		    wallet: "test"
		  -
		    name: "b"
		    model: "gpt-neo-125M"
		    port: 8093
		    keyfile: 1
		    wallet: "test"
		  -
		    name: "c"
		    model: "gpt-neo-125M"
		    port: 8094
		    keyfile: 2
		    wallet: "test"
		  -
		    name: "d"
		    model: "gpt-neo-125M"
		    port: 8095
		    keyfile: 3
		    wallet: "test"
		machine2:
		  -
		    name: "i"
		    model: "gpt2"
		    port: 8096
		    keyfile: 4
		    wallet: "test"
		  -
		    name: "j"
		    model: "gpt-neo-125M"
		    port: 8097
		    keyfile: 5
		    wallet: "test"
		  -
		    name: "k"
		    model: "gpt-neo-125M"
		    port: 8098
		    keyfile: 6
		    wallet: "test"
		  -
		    name: "l"
		    model: "gpt-neo-125M"
		    port: 8099
		    keyfile: 7
		    wallet: "test"
		

The configuration above represent mining architecture for two machine each with 4 GPUs.

Step 2:

	Create Keys:
		
		python3 create_keys.py
		

Step 3: 

	Copy keys to each machine:
		
		scp -r autominer <user>
		

Step 4:

	Install PM2 & TMUX:
		
		sudo apt update
		sudo apt upgrade
		sudo apt install npm -y
		sudo npm install pm2@latest -g
		sudo apt install tmux
		

Step 5:

	Open TMUX:
		
		tmux
		

Step 6: 

	Run auto miner (once per machine. Be sure to set the ENVAR:

		MACHINE_ID=machine1 python3 auto.py
		MACHINE_ID=machine2 python3 auto.py
		etc...
Step 7: 
	
Turn on the trust monitor (this feature is still experimental) 
		
		python3 trust_monitor.py
		
		
		
**ROADMAP auto.py:**
*Features currently in production*
1. Prompt use for registration settings.
                                       Ex: Would you like to:
                                            a) set TPB to 256 is a card is already serving a hotkey?
                                            b) set TPB to 128 is a card is already serving a hotkey?
                                            c) set TPB to 128 is a card is already serving a hotkey?
                                            d) yurn registration off for all cards already serving a hotkey?			    
2. Prompt user for discord API key for notifications.
                                        	    Ex: Would you like to turn on notifcations for your discord server?
                                                         a) yes
                                                         b) no
                                                         If yes, what is your API key:
							 
							 
							 
**ROADMAP trust_monitor.py:**
*Features currently in production:*
1. Prompt user for a network.
                            Ex: What network would you like to use:
                                 a) nobunaga
                                 b) nakamoto
                                 c) local
                                 If C, would you like to use a specific endpoint
                                 a) no
                                 b) yes
                                 If yes, which endpoint would you like to use?			 
2. Prompt user for their disocrd API key:
                                          # What is your discord API key:				  
# 3. Do not monitor keys outside the ImmunityPeriod.
# 4. Prompt the user for a TRUST_SCORE_THRESHOLD (defaults to .5)
# 5. If a key returns a trust score less than the TRUST_SCORE_THRESHOLD, do not ping the user for another 5-20 minutes. - This is somewhat working already



**Advanced Features not currently in (production auto.py):**
1. Notify user every time a Server times out on a request. Provide a csv file of the logs and which peer they timed out on.
2. Add prompt to blacklist specific keys upon startup

**Advanced Features not currently in production (trust_monitor.py):**
1. Give the user a graph of trust over the last 12 hours everytime a key drops below the threshold
		
  
