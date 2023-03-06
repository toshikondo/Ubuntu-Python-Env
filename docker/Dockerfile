FROM ubuntu:20.04

#ENV DEBIAN_FRONTEND noninteractive

# Set time zone
ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install packages
RUN apt update 
RUN apt install -y \
    curl \
    git \
    vim \
    openssh-server

# Change .bashrc
COPY .bashrc /
RUN mv .bashrc ~/.bashrc

# Enable ssh access from client
RUN mkdir /var/run/sshd
RUN echo 'root:mypassword' | chpasswd
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]


############################################################################################### 
# 1. cd ~/Ubuntu-Python-Env/docker
# 2. $docker build . -t <image name>
# 3. $docker run -it -p 50022:22 -v ~/Ubuntu-Python-Env/PermanentData:/root/PemanentData -d <image name> 
# 
# 4. Login remote device
#    ssh root@<ip address of docker host > -p:50022
#    password:mypassword
###############################################################################################











