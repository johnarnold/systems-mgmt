#Build Jenkins data container:

    sudo docker build -t jenkins-data jenkins-data/.

#Run data container

    sudo docker run --name=jenkins-data jenkins-data

#Build Jenkins master:

    sudo docker build -t jenkins-master jenkins-master/.

#Run Jenkins Master:

    sudo docker run -d -p 8080:8080 -p 50000:50000 --volumes-from jenkins-data --name jenkins-master jenkins-master


#Build NGINX proxy:

    sudo docker build --tag nginx-proxy nginx-reverse-proxy-ssl/.

#Run Proxy:

    sudo docker run -d -p 443:443 -p 80:80 --name myproxy --link jenkins-master:upstream nginx-proxy

#Build slave image:

    sudo docker build -t slave sonic-slave

#Add the jenkins user:

    sudo useradd -d /home/jenkins jenkins -m -s /bin/bash
    sudo mkdir /home/jenkins/.ssh
    sudo cp jenkins-id_rsa.pub /home/jenkins/.ssh/authorized_keys
    sudo  chown -R jenkins /home/jenkins
    sudo chgrp -R jenkins /home/jenkins
    sudo chmod 600 /home/jenkins/.ssh/authorized_keys
    sudo chmod 700 /home/jenkins/.ssh

    sudo groupadd docker
    sudo usermod -aG docker jenkins
