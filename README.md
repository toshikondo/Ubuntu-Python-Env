# Ubuntu-Python-Env

## This is Docker container for Python environment based on Ubuntu 20.04
### How to use 
1. git clone https://github.com/toshikondo/Ubuntu-Python-Env.git
2. cd ~/Ubuntu-Python-Env
3. $docker build -f ./docker/Dockerfile ./docker -t \<docker image\>
4. $docker run -p 50022:22 -v ~/Ubuntu-Python-Env/PermanentData:/root/PemanentData -d \<docker image name or ID\>  
5. Login remote device  
   ssh root@\<ip address of docker host\> -p 50022  
   password: mypassword

\* PermanetData directory on host is mounted /root/PemanentData on container.  