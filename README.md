# Initia Node Deployment
This repository contains Ansible scripts for the installation, updating, and removal of an Initia node on Linux systems. The playbooks are designed to simplify the process of setting up an Initia node, managing its services, and ensuring seamless node operations.

## Prerequisites
Recommended:

System: Linux Ubuntu 22.04
CPU: 4-core
RAM: 16GB
Storage: 1TB SSD
You will need a VPS 3 server for hosting an Initia node. We recommend Contabo for its reliability and performance. For a guide on setting up a Contabo VPS server, you can refer to the Contabo VPS Server Guide.

Getting Started
## Step 1: Installing Dependencies
Update your system's package list and install necessary tools:


```
sudo apt update && sudo apt upgrade -y
sudo apt install git ansible -y

```
Ensure you have Ansible version 2.15 or newer:

```
ansible --version

```
## Step 2: Downloading the Project
Clone this repository to access the Ansible playbook and all necessary files:


```
git clone https://github.com/nodemasterpro/deploy-node-initia.git
cd deploy-node-initia
```

## Step 3: Installing the Initia Node
Execute the playbook using the following command. During this process, you will be prompted to enter the values for moniker (node name) and snapshot_block (the block height of the Polkachu snapshot).


```
ansible-playbook install_initia_node.yml

```
Example of input prompts:

```
Enter the node name: mynode
Enter the block height of the polkachu snapshot: 1234567
```

## Step 4: Viewing Node Logs
To view the logs for the Initia node:

```
journalctl -u initia-node -f -o cat
```
To exit the logs, type Ctrl+C.

## Step 5: Creating an Initia Wallet
After installing the node, create an Initia wallet essential for network operations:

```
ansible-playbook create_initia_wallet.yml
```
Once completed, you will obtain the address of the Initia wallet. Save it for requesting testnet funds and further operations.

## Step 6: Requesting Initia Testnet Funds
To request testing funds on the Initia network, check the #faucet-verification channel on the Initia Discord. Then, go to the Initia faucet website and claim test tokens by typing your wallet number.

Note: Due to high demand, you may need to wait 20 minutes for the tap role to be checked. You can only claim 30 INIT once every 24 hours.

## Step 7: Checking Node Synchronization
To ensure your node is fully synchronized with the Initia blockchain:

```
initiad status | jq
```

Synchronization takes several hours. Once the catching_up variable is false, your node is fully synchronized and ready for further operations.

## Step 8: Registering the Initia Node as a Validator
Finalize your node configuration by registering your node as a validator and linking it to your Initia wallet. Ensure your node is synchronized with the blockchain and you hold Initia tokens in your wallet. Then, run this command:


```
ansible-playbook register_initia_node.yml
```
During this step, you will be prompted to input the following information:

Moniker: "node_name"
Details: "a phrase of your choice"
Website: "your website"

## Step 9: Viewing Validator State
You can check the status of your validator by executing:

```
initiad query mstaking validator <validator_address>
```
Replace <validator_address> with your validator's wallet address provided at the end of the playbook execution.

## Step 10: Setting Up the Oracle
To set up the Oracle for Initia, execute the following playbook:

```
ansible-playbook setup_oracle.yml
```
This will configure and run the Oracle sidecar, enabling essential components for the Oracle and Market functionalities.

## Additional Information
Stopping the Service
To stop the Initia node:
```
sudo systemctl stop initia-node
```

Starting the Service
To start the Initia node:
```
sudo systemctl start initia-node
```

Removing the Initia Node
To remove the Initia node, run the playbook for removal:
```
ansible-playbook remove_node_initia.yml
```
Ensure to back up any important data before removing the node, as this action may delete node data.

Conclusion
That's it! You have successfully deployed an Initia node, thus contributing to the robustness of the network and earning potential rewards. Join the Initia community on Discord and Twitter to stay informed about the project.

Thank you for taking the time to read this guide. If you have any questions or would like to continue the conversation, feel free to join the Initia community on Discord.

Stay updated and connected: Follow us on Twitter, join our Telegram group, Discord server, and subscribe to our YouTube channel.









