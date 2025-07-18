# Wazuh
Wazuh is a free, open-source security platform that monitors systems, detects threats, analyzes logs, and ensures compliance. It combines `SIEM` ( Security Information and Event Management ) and `HIDS`( Host-based Intrusion Detection System ) capabilities to protect endpoints and servers in real time.
- Threat detection
- Log analysis
- Intrusion detection
- File integrity monitoring
  
### Wazuh Manager And Dashboard
currently Wazuh supports the following operating system versions:

- Ubuntu 16.04  
- Ubuntu 18.04  
- Ubuntu 20.04  
- Ubuntu 22.04  
- Ubuntu 24.04  
- Red Hat Enterprise Linux 7  
- Red Hat Enterprise Linux 8  
- Red Hat Enterprise Linux 9  
- CentOS 7  
- CentOS 8  
- Amazon Linux 2  
- Amazon Linux 2023  

### Installation procees
### Step 1
Make sure you have curl installed if not then use the following command:

```
sudo apt update -y
sudo apt install curl -y
```
### Step 2
To install Wazuh Manager and Dashboard on Ubuntu 22.04, use:

```
sudo curl -sO https://packages.wazuh.com/4.5/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```
### Step 3

After installation, access the dashboard and log in using the default admin user.

- `User : admin`
- `Password : <ADMIN_PASSWORD>`

Access Wazuh-Dashboard:

- `https://<WAZUH_DASHBOARD_IP_ADDRESS>`
- `https://localhost`


If you forgot your password then use this command

```
sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
```
### Step 4

To check Wazuh-Manager status:
```
sudo systemctl status wazuh-manager
sudo systemctl status wazuh-dashboard
sudo systemctl status filebeat
```

If not started use the following command to start
```
sudo systemctl start wazuh-manager
sudo systemctl start wazuh-dashboard
sudo systemctl start filebeat
```

To enable wazuh at start up 
```
sudo systemctl enable wazuh-manager
sudo systemctl enable wazuh-dashboard
sudo systemctl enable filebeat
```
### To manage agents
```
sudo /var/ossec/bin/manage_agents
```
### To see active agents
```
sudo /var/ossec/bin/agent_control -l
```

### Uninstalling Process

### Step 1
Stop Wazuh
```
sudo systemctl stop wazuh-manager
sudo systemctl stop wazuh-dashboard
sudo systemctl stop filebeat
sudo systemctl stop wazuh-indexer
```

### Step 2
Disable wazuh at start up
```
sudo systemctl disable wazuh-manager
sudo systemctl disable wazuh-dashboard
sudo systemctl disable filebeat
sudo systemctl disable wazuh-indexer
```

### Step 3
Remove config
```
sudo rm -rf /var/ossec
sudo rm -rf /etc/filebeat
sudo rm -rf /usr/share/wazuh-dashboard
sudo rm -rf /etc/wazuh-indexer
sudo rm -rf /var/lib/wazuh-indexer
sudo rm -rf /usr/share/wazuh-indexer
sudo rm -rf /var/log/wazuh-indexer
```
Uninstall wazuh Packages
```
sudo dpkg --purge wazuh-manager wazuh-dashboard filebeat wazuh-indexer
```

### Step 4
Verify uninstallation
```
dpkg -l | grep wazuh
```

# Wazuh-agent
### Installing Wazuh Agent
Wazuh agents are software components installed on the endpoints or end devices (servers, workstations, cloud instances, etc.) you want to monitor. 
They collect security data and log information from the host system and send it to the Wazuh Manager for analysis and further processing.

I will be using Debian Machine for Wazuh Agent

Run the following command in your debian machine ,Make sure you have curl installed

### step 1
```
sudo curl -s https://raw.githubusercontent.com/iamsinnerr/wazuhh/main/Linux-Install.sh | bash
```

This script fetches and installs the latest supported agent version. 
You can inspect the script here [Linux-Install](https://github.com/i-am-paradoxx/wazuh-linux/blob/main/Linux-Install.sh)

### Step 2
Start and Enable Wazuh-agent
```
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```
Check for status
```
sudo grep ^status /var/ossec/var/run/wazuh-agentd.state
```

### Uninstalling Wazuh-Agent
### step 1
Stop and Disable Wazuh Agent
```
sudo systemctl stop wazuh-agent
sudo systemctl disable wazuh-agent
```
### Step 2
Remove Wazuh Agent
```
sudo dpkg --purge wazuh-agent
sudo rm -rf /var/ossec
```
### Step 3 
Verify Uninstallation
```
dpkg -l | grep wazuh
```
visit [Wazuh Documentaion](https://documentation.wazuh.com/current/getting-started/index.html) for more details.
# Credits

This project makes use of resources and code from:

- [Wazuh GitHub Repository](https://github.com/wazuh/wazuh)
- [Wazuh Official Website](https://wazuh.com)

I thank the Wazuh team for their contributions to the open-source community.


