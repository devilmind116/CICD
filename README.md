Create a default VPC on your default AWS region

```
aws ec2 create-default-vpc
```

Create Key Pair and save the PEM file

```
aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem
```

Create the terraform scripts

```
terraform init
terraform plan
terraform apply --auto-approve
```

Note down the outputs from Terraform execution

```
ACCESS_YOUR_JENKINS_HERE = "http://34.207.188.28:8080"
Jenkins_Initial_Password = "sudo cat /var/lib/jenkins/secrets/initialAdminPassword"
MASTER_SERVER_PRIVATE_IP = "172.31.59.233"
MASTER_SERVER_PUBLIC_IP = "34.207.188.28"
```

To get the Jenkins initial password
- SSH to the MASTER_SERVER EC@ instance.
- And paste the output from the --> sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Now lets work on creating the Slave Nodes

Create the slave.tf terraform script

```
terraform plan
terraform apply --auto-approve
```

Note down the output from these scripts

```
NODE_SERVER_PRIVATE_IP = "172.31.62.61"
NODE_SERVER_PUBLIC_IP = "54.210.86.240"
```

Now SSH to NODE_SERVER

- Reset the password
- Edit SSH setting to allow password based authentication and to permit root login
```
sudo -i
passwd ec2-user
vi /etc/ssh/sshd_config
service sshd restart
```
Remove '#' before "AllowPasswordBasedAuthentication" and "PermitRootLogin"

Now lets generate a SSH key in Master Server
```
sudo -i
passwd ec2-user
ssh-keygen ##Hit enter thrice
ssh-copy-id ec2-user@NODE_SERVER_PRIVATE_IP # Replace NODE_SERVER_PRIVATE_IP with the IP of your node
```

And now you can SSH Node server through Master server
```
ssh 'ec2-user@NODE_SERVER_PRIVATE_IP'
```

Splunk Setup

- Allow seamless start for every boot up of server
```
sudo /opt/splunk/bin/splunk enable boot-start
```

- Allow incoming SSH traffic through the UFW (Uncomplicated Firewall) on your Ubuntu system
```
sudo ufw allow openSSH
```

- Allow incoming traffic from 8000
```
sudo ufw allow 8000
```

- Check UFW status and enable if inactive
```
sudo ufw status
sudo ufw enable
```

- Start the Splunk
```
sudo /opt/splunk/bin/splunk start
```


  
