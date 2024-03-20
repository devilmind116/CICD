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
