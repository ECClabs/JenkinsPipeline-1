#!/bin/bash

echo "Installing Jenkins 2.452.2 and Java 17... Please wait."

{
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

} &> /dev/null

if [ $? -eq 0 ]; then
  echo "✅ Jenkins 2.452.2 and Java 17 installed successfully!"
else
  echo "❌ Installation failed. Please try the following:"
  echo "1️⃣ Check internet connectivity inside the EC2 instance."
  echo "2️⃣ Make sure this URL is accessible:"
  echo "    https://pkg.jenkins.io/redhat-stable"
  echo "3️⃣ Run the script again: ./install_jenkins.sh"
  echo "4️⃣ If it still fails, contact your lab instructor or admin."
fi
