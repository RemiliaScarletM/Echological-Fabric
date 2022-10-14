[//]: # (SPDX-License-Identifier: CC-BY-4.0)

# Hyperledger Fabric For Echologicol Sound

## Environment Set Up For Development Environment
1. Setup environment  
`sudo apt update`   
`sudo apt upgrade`   
`sudo apt install git jq curl docker.io`   
`rm -rf /usr/local/go && tar -C /usr/local -xzf go1.18.2.linux-amd64.tar.gz`  
`export PATH=$PATH:/usr/local/go/bin`  
After doing the previous step, please find whether the version of go is 1.18.2 by 
`go version`
and it should be `go version go1.18.2 linux/amd64`  


2. Clone hyperledger fabric through github and cd to it  
`git clone https://github.com/miaopasei/Echological-Fabric.git`  
Direct to the directory fabric-echological  
 `chmod -x bootstrap.sh`  
 `sudo bash bootstrap.sh`  
 It will be suceed if it list all of the docker image.

 3. Test the environment
 `cd network-test`  
 `sudo ./network.sh up`  
 `sudo ./network.sh createChannel`  
 `sudo docker ps`  
 If success, you can see three docker container which are two fabric-peer and one fabric-orderer 

## Helper For Echologicol Project  
Tips: Our project is in the director called echological-chaincode  
1. If you have other node for test version, please use `sudo ./network.sh down` before launching.  
2. Use `sudo ./network.sh up` and `sudo ./network.sh createChannel`  to update the container to update the container.  
3. Use `./network.sh deployCC -ccn basic -ccp ../echological-chaincode -ccl go` and script will automatically start our chain.  
4. Set up basic enviorment variables:
```
export PATH=${PWD}/../bin:$PATH
export FABRIC_CFG_PATH=$PWD/../config/
```
5. You can use moveToOrg1.sh/moveToOrg2.sh to change your peer node
```
source moveToOrg1.sh
```

6. Run the simple query functions
```
peer chaincode query -C mychannel -n basic -c '{"Args":["GetAllUsers"]}'
```
7. If you need to edit the asset on the chain, use "invoke" to call functions:
```
peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls --cafile "${PWD}/organizations/ordererOrganizations/example.com/orderers/orderer.example.com/msp/tlscacerts/tlsca.example.com-cert.pem" -C mychannel -n basic --peerAddresses localhost:7051 --tlsRootCertFiles "${PWD}/organizations/peerOrganizations/org1.example.com/peers/peer0.org1.example.com/tls/ca.crt" --peerAddresses localhost:9051 --tlsRootCertFiles "${PWD}/organizations/peerOrganizations/org2.example.com/peers/peer0.org2.example.com/tls/ca.crt" -c '{"function":"CreateUser","Args":["Name","UserID","Email","UserType","0.0"]}'
```

8. move to node 2, now you can get new User:
```
source moveToOrg2.sh
peer chaincode query -C mychannel -n basic -c '{"Args":["GetAllUsers"]}'
```


## License <a name="license"></a>

Hyperledger Project source code files are made available under the Apache
License, Version 2.0 (Apache-2.0), located in the [LICENSE](LICENSE) file.
Hyperledger Project documentation files are made available under the Creative
Commons Attribution 4.0 International License (CC-BY-4.0), available at http://creativecommons.org/licenses/by/4.0/.
