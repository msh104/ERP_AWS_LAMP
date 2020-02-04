# How to set up an ERP/CRM system on a LAMP stack using EC2 and RDS.
Sign into AWS
Open EC2
Click Instances on Left Side
Click "Launch Instance"
Select "Amazon Linux AMI 2016.09.1 (HVM), SSD Volume Type"
Select Free Tier
Click review and launch
Press Launch
Create Pair
Download Pair
Launch Instance
Open list of Instances
Swap in your file name: chmod 400 ServerPair.pem
Swap in your file name and ip address: ssh -i "ServerPair.pem" ec2-user@ec2-54-152-134-146.compute-1.amazonaws.com
Update your instance sudo yum update -y
