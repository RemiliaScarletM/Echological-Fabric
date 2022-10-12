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


## License <a name="license"></a>

Hyperledger Project source code files are made available under the Apache
License, Version 2.0 (Apache-2.0), located in the [LICENSE](LICENSE) file.
Hyperledger Project documentation files are made available under the Creative
Commons Attribution 4.0 International License (CC-BY-4.0), available at http://creativecommons.org/licenses/by/4.0/.
