# apache-webserver


Prerequisites
A user account with sudo privileges
Access to a command line terminal (menu > application > utilities > terminal)
The yum package manager, installed by default

Installing Apache on CentOS
Step 1: Update Software Versions List
Ensure you are using the latest versions of the software. In a terminal window, input the command:

sudo yum update
The system should reach out to the software repositories and refresh the list to the latest versions.

Step 2: Install Apache
To install Apache on your CentOS server, use the following command:

sudo yum install httpd
The system should download and install the Apache software packages.

Step 3: Activate Apache
To activate Apache, start its service first.

1. Enter the following command in a terminal window:

sudo systemctl start httpd
This will start the Apache service.

2. Next, set the Apache service to start when the system boots:

sudo systemctl enable httpd

Step 4: Verify Apache Service
Display information about Apache, and verify it’s currently running with:

sudo systemctl status httpd
verifying the apache service is running

Step 5: Configure firewalld to Allow Apache Traffic
In a standard installation, CentOS 7 is set to prevent traffic to Apache.

Normal web traffic uses the http protocol on Port 80, while encrypted web traffic uses the https protocol, on Port 443.

1. Modify your firewall to allow connections on these ports using the following commands:

sudo firewall-cmd ––permanent ––add-port=80/tcp
sudo firewall-cmd ––permanent ––add-port=443/tcp
2. Once these complete successfully, reload the firewall to apply the changes with the command:

sudo firewall-cmd ––reload
Step 6: Configure Virtual Hosts on CentOS 7 (optional)
Virtual hosts are different websites that you run from the same server. Each website needs its own configuration file.

Make sure these configuration files use the .conf extension, and save them in the /etc/httpd/conf.d/ directory.

There are a couple of best practices to use when you’re setting up different websites on the same server:

Try to use the same naming convention for all your websites. For example:
/etc/httpd/conf.d/johnlord.conf
Use a different configuration file for each domain. The configuration file is called a vhost, for a virtual host. You can use as many as you need. Keeping them separate makes troubleshooting easier.
1. To create a virtual host configuration file, enter the following into a terminal window:

sudo vi /etc/httpd/conf.d/johnlord.conf
This will launch the Vi text editor, and create a new vhost.conf file in the /etc/httpd/conf.d directory.

2. In the editor, enter the following text:

<VirtualHost 192.168.0.100:80>
ServerAdmin webmaster@johnlord.com
DocumentRoot /var/www/johnlord
ServerName johnlord.com
ServerAlias www.johnlord.com
CustomLog /var/log/johnlord.com-access_log common
ErrorLog /var/log/johnlord.com-error_log
</VirtualHost>

Save the file and exit.

3. Next, enter the following command to create a directory for you to store your website files in:

sudo mkdir /var/www/johnlord/
vim /johnlord/index.html

then go to /var/log/httpd to enter your custom logs and error logs
touch johnlord.com-access_log access_log-20201229  error_log-20201229  johnlord.comm-error_log

4. Restart the Apache service to apply your changes by entering:

sudo systemctl restart httpd



Commands For Managing Apache Service
Other commands that you can use to control the Apache service include:

Stop Apache Service:

sudo systemctl stop httpd
Prevent or disable Apache from starting when the system boots:

sudo systemctl disable httpd
Re-enable Apache at boot:

sudo systemctl enable httpd
Restart Apache and apply any changes you have made:

sudo systemctl restart httpd

