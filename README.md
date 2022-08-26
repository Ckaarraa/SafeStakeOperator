# Project SafeStake Operator Node

**Description**:  
SafeStake is a decentralized validation framework for performing ETH2 duties and its backend is designed on top of Lighthouse (ETH2 consensus client) and Hotstuff (a BFT consensus library).

## Dependencies
### Server 

 * Public Static Network IP 
 * Hardware(recommend)
   * CPU: 4
   * Memory: 8G
   * Disk: 500GB
 * OS
   * Unix
 * Software
   * Docker
   * Docker Compose 

### Set firewall rule
![firewall rule](https://github.com/ParaState/SafeStakeOperator/blob/main/imgs/firewall_rule.png?raw=true)

## Installation

### Login your server([jumpserver](https://www.jumpserver.org/) recommand)
### Install Docker and Docker compose
* [install docker engine](https://docs.docker.com/engine/install/)
* [install docker compose](https://docs.docker.com/compose/install/)

### Start your docker engine
```
sudo systemctl start docker
```

### Create local volume directory

```
 sudo mkdir -p /data/geth
 sudo mkdir -p /data/lighthouse
 sudo mkdir -p /data/jwt
 sudo mkdir -p /data/operator
```
### Generate your jwt secret to jwt dirctory

```
openssl rand -hex 32 | tr -d "\n" | sudo tee /data/jwt/jwtsecret
```
### Clone operator code from github

```
git clone --recurse-submodules https://github.com/ParaState/SafeStakeOperator.git dvf
```

### Fill enr you get in testnet.xyz
enr configure 

**It has default value in latest source code**

```
cd dvf
vim .env
```
### Build operator images
```
sudo docker compose -f  docker-compose-operator.yml build
```

## Run
### Run your operator
```
sudo docker compose -f  docker-compose-operator.yml up -d
```

### Wait for geth data ready
maybe 24 hours later
### Get your operator public key
```
sudo docker compose -f docker-compose-operator.yml logs -f operator | grep "node public key"
```
output
> dvf-operator-1  | [2022-08-13T16:01:33.814Z INFO  dvf::node::node] node public key Al0wMNz3JpkYDH7HVp93dZfLMt1GJHypLfhwOWS0NwC/

### Back up your operator private key file
path

```
/data/operator/ropsten/node_key.json
```
