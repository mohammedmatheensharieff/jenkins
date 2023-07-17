FROM ubuntu

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y openssh-server && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir /var/run/sshd && \
    chmod 0755 /var/run/sshd && \
    ssh-keygen -A

RUN useradd -m remote_user && \
    echo "remote_user:1738" | chpasswd && \
    mkdir /home/remote_user/.ssh && \
    chmod 700 /home/remote_user/.ssh

COPY openssh.pub /home/remote_user/.ssh/authorized_keys

RUN chown remote_user:remote_user -R /home/remote_user/.ssh/ && \
    chmod 600 /home/remote_user/.ssh/authorized_keys

RUN apt-get update && \
    apt-get install mysql-client -y

RUN apt-get update && \
    apt-get install awscli -y

RUN ssh-keygen -A

CMD /usr/sbin/sshd -D 
