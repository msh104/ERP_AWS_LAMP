# How to set up an ERP/CRM system on a LAMP stack using EC2 and RDS.
1.  Sign into AWS
2.  Open EC2
3.  Click Instances on Left Side
4.  Click "Launch Instance"
5.  Select "Amazon Linux AMI 2016.09.1 (HVM), SSD Volume Type"
6.  Select Free Tier
7.  Click review and launch
8.  Press Launch
9.  Create Pair
10.  Download Pair
11.  Launch Instance
12.  Open list of Instances
13.  Swap in your file name: chmod 400 ServerPair.pem
14.  Swap in your file name and ip address: ssh -i "ServerPair.pem" ec2-user@ec2-54-152-134-146.compute-1.amazonaws.com
15.  Update your instance sudo yum update -y
