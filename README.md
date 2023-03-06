# Ubuntu-Python-Env
## How to use 
1. cd ~/Ubuntu-Python-Env/docker
2. $docker build . -t \<image name\>
3. $docker run -it -p 50022:22 -v ~/Ubuntu-Python-Env/PermanentData:/root/PemanentData -d \<image name\>  
4. Login remote device  
   ssh root@\<ip address of docker host\> -p:50022  
   password: mypassword

   \* PermanetData directory on host is mounted /root/PemanentData on container.  