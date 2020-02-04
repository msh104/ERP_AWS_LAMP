# How to set up an open source ERP/CRM system on a LAMP stack using EC2 and RDS.

Please view these same instructions I wrote and contributed to on: https://wiki.dolibarr.org/index.php/Cloud_with_Amazon_EC2#Manual_process_from_scratch

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
16.  Install Apache Web Server, MySQL, PHP sudo yum install -y httpd24 php70 mysql56-server php70-mysqlnd php70-intl php70-gd
17.  Start the Apache Web Server sudo service httpd start
18.  Make it so Apache Web Server runs on server boot: sudo chkconfig httpd on
19.  Verify it with: chkconfig --list httpd and httpd 0:off 1:off 2:on 3:on 4:on 5:on 6:off
20.  Go to your Public DNS or IPv4 Public IP: Example: ec2-54-123-134-146.compute-1.amazonaws.com
21.  Create a new user group sudo groupadd www
22.  Add our EC2 User to this group sudo usermod -a -G www ec2-user
23.  Leave the current session exit.  If you do not exit here, this will not work.
24.	Sign back in. Swap in your file name and ip address: ssh -i "ServerPair.pem" ec2-user@ec2-54-123-134-146.compute-1.amazonaws.com
25.	Verify www exists by running: groups
26.	Give www permission on server files /var/www with: sudo chown -R root:www /var/www
27.	Change file permissions: “sudo chmod 2775 /var/www” and “find /var/www -type d -exec sudo chmod 2775 {} \;”
28.	Add a index.html in var/www/html: “touch /var/www/html/index.html” and “vi /var/www/html/index.html”, then add some content, such as "Hello, Mike!" or "Mike's World!".
29.	Go back to Instances, scroll right and look at the Security Groups column and make note of the name; the name's format should be similar to that of "launch-wizard-3".  Another method that can be used is selecting your Instance > Change Security group and make note of the name.
30.	(basically what I said in the instructions above) Right click on your new instance, select Networking, then Change Security Group
31.	Open Security Groups on the left side bar: https://console.aws.amazon.com/ec2/
33.	Select the group, go to Actions > Edit the Inbound rules for that security group already assigned.
34.	Add Rule and set the type to be HTTP
35.	Files sit in ls -l /var/www
36.	Go to your IPv4 and you should see the content you created eariler, such as “Hello, Mike!”.
- Download open source ERP/CRM software here: https://www.dolibarr.org/downloads
- Upload all files from dolibarr_version_number_xxx/htdocs into the folder with index.html on AWS.  You now must rename index.html to another name.  This upload will take a few minutes.  Make sure that all the files are placed in the same folder as the index file (i.e. /var/www/html/index.html).  Rename or remove the index.html file to not block the index.php file.
- You will now need to create your MySQL database on AWS.  Go to AWS > Services > RDS > Create db > Standard Create > MySQL > - Keep at Version 5.7.2.2 > Free tier > record down the settings as it will come in hand for the ERP setup.  For example, the db name will be in the format of “database-2”, master username and password, and keep all else the same and click on “Create database”.  This will now take a few minutes to launch.
- Once it’s done creating, go into Terminal (if on a Mac, or Command Prompt on Windows), remote to EC2, and check if mysql is on by using the command “sudo service mysqld status”.  If mysql is stopped, type “sudo service mysqld start”.  
- Go back into RDS: click on the name (“database-2”), grab the endpoint which is similar to the format of “database-2.xxx.rds.amazonaws.com“, finish your setup.
- To fix this error that may appear “…htdocs/conf/conf.php does not exist…create permissions”, navigate to the conf folder (it is not under htdocs as I have found some instructions have stated, but actually under html), then use these commands: “touch conf.php”, “chmod 666 conf.php”, and “sudo service httpd restart” to restart Apache.
- Create folder “documents” in html folder and give server write access to it: “mkdir documents”, “chmod 777 documents” (you can use other privileges other than 777 to restrict access and make this folder "safer"), and “sudo service httpd restart”.
- On this next install page ("Directory to store uploaded and generated documents"), place a check on the checkbox "Create database", create the "Login" user name is "root" and the password is the master password that was set up in AWS' RDS.
- Under "Database server- Superuser access", create the "Login" user name of "root" again and the same password as the previous step.
- If successful, you will see the "Configuration file" screen with a number of green check marks.
- Click on Next Step, and you will see this message “The current step may take several minutes. Please wait until the next screen is shown completely before continuing.  Please be patient...
- If everything is successful, you will see a new screen title "Database" and green check marks.
- On the following screen, create your admin login here on the "Dolibarr admin login" screen, and click the Next button.
- Congratulations.  If you now see the message "Dolibarr install or upgrade- End of setup." and "This installation was completed successfully", you have completed the install.
- Finally, create the install.lock file.  This file prevents other users from reinstalling the app.  Navigate to the “install” folder, and on Linux use the command “touch install.lock”





