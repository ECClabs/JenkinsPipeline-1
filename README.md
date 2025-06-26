#!/bin/bash


sudo tee /etc/yum.repos.d/jenkins.repo > /dev/null <<EOF
[jenkins]
name=Jenkins-stable
baseurl=https://pkg.jenkins.io/redhat-stable
gpgcheck=1
gpgkey=https://pkg.jenkins.io/redhat/jenkins.io.key
EOF


sudo rpm --import https://pkg.jenkins.io/redhat/jenkins.io.key


sudo yum clean all -y
sudo yum makecache -y


sudo yum install java-17-amazon-corretto -y


sudo yum install jenkins-2.452.2 -y

echo "✅ Jenkins 2.452.2 installation complete!"
echo "🌐 Access it at: http://<your-elastic-ip>:8080"
