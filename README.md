#!/bin/bash


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
  echo " Jenkins and Java installed successfully!"
else
  echo "❌ Installation failed."
  echo ""
  echo "👉 Try the following steps to resolve:"
  echo "1️⃣ Run the command below to clean cached files (optional, only if script fails again):"
  echo "    sudo yum clean all && sudo yum makecache"
  echo "2️⃣ Then re-run the script:"
  echo "    ./install_jenkins.sh"
  echo "3️⃣ If the error still comes, restart the EC2 instance and try again."
  echo "4️⃣ Make sure you are connected to the internet inside the EC2 instance."
  echo ""
  echo "📣 If it still fails after retrying, contact your lab instructor or admin for help."
fi
