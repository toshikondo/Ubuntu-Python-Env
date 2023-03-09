FROM ubuntu:20.04

#ENV DEBIAN_FRONTEND noninteractive

##### Set time zone #####
ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

##### Install packages #####
RUN apt update && apt install -y \
    curl \
    git \
    vim \
    openssh-server \
    python3-pip 

##### Change .bashrc #####
COPY .bashrc /
RUN mv .bashrc ~/.bashrc

##### Download and install python3.9.16 #####
WORKDIR /root
RUN apt install -y --no-install-recommends wget build-essential libreadline-dev \ 
libncursesw5-dev libssl-dev libsqlite3-dev libgdbm-dev libbz2-dev liblzma-dev zlib1g-dev uuid-dev libffi-dev libdb-dev
RUN wget --no-check-certificate https://www.python.org/ftp/python/3.9.16/Python-3.9.16.tgz \
&& tar -xf Python-3.9.16.tgz \
&& cd Python-3.9.16 \
&& ./configure --enable-optimizations\
&& make \
&& make install \
&& cd .. \
&& rm -f Python-3.9.16.tgz
COPY requirements.txt /root
RUN python3.9 -m pip install -r requirements.txt
RUN echo 'alias python=python3.9' >> ~/.bashrc

##### Enable ssh access from client #####
RUN mkdir /var/run/sshd
RUN echo 'root:mypassword' | chpasswd
RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile
EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]


############################################################################################### 
# How to use
# 1. cd ~/Ubuntu-Python-Env/docker
# 2. $docker build . -t <docker image>
# 3. $docker run -it -p 50022:22 -v ~/Ubuntu-Python-Env/PermanentData:/root/PemanentData -d <docker image> 
# 
# 4. Login remote device
#    ssh root@<ip address of docker host> -p:50022
#    password:mypassword
#
#  PermanetData directory on host is mounted /root/PemanentData on container.  
###############################################################################################
