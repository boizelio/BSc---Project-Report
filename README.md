# **BSc---Project-Report**

## **Introduction**

This report is about installing and configuring a virtual machine hosting a LAMP stack, an open-source Web development platform, that uses Linux as the operating system, Apache as the Web server, MySQL as the RDBMS and PHP as the object-oriented scripting language.
The report presentes the step-by-step from Configuring and deploying of the virtual machine to the introdction of the wordpress interface.

## **Virtualization concept**

To fully understand the concept of technology, develop a parallel between what is real and what is virtual. Following this line of reasoning, something real physical, concrete qualities; The virtual is associated with what is simulated, abstract. In this way, a virtualization can be defined as a creation of a virtual environment that simulates a real environment, propitiating a use of several systems and applications without a physical physical need on a qualified host machine ....
In layman's terms virtualization is often:
 	-The creation of many virtual resources from one physical resource.
	-The creation of one virtual resource from one or more physical resource

## **Virtual box concept**

VirtualBox is a "virtualization software" that allows you to install and run different operating systems on a single computer. That is, virtual computers running within a single real computer. Virtual Box will be used for the creation of the virutal machine of this project.

## **Web server and Apache**

Web servers are responsible for storing and exchanging information with other machines. Because of this, at least two participants are involved in each exchange of information: one customer, who requests information, and one server, who responds to those requests. Each side also requires a specialized program to negotiate an exchange of data; In the case of the client, a browser like Internet Explorer is used.
On the server side there are several software options available, but all have a similar task: negotiate transfers of data between clients and servers via Hypertext Transfer Protocol (HTTP), the Web communications protocol. The software depends on the chosen operating system To the server. For example, Microsoft IIS is a popular choice for Windows, and Unix fans already choose Apache.
Like any type server, Apache is responsible for providing pages and all resources that can be accessed by the user. Sending of emails, messages, online purchases and several others. What's worth noting is that Apache is, after all, distributed under a GNU license, that is, free.

## **Configuration of the virtual machine**

1.	On the Virtual Box main screen, click the "New" button.

2.	The next step will be to give a name to the virtual machine and choose the type of the operating system. I gave the name of Ubunto, in Operating System I chose Linux and in version, extremely important step, I chose the 32 Bits version.

3.	Click “Next” and select the amount of memory for the new environment. Here I will leave with 2 Gigabytes (1048 Megabytes), but one tip is not to exceed 50% of the total memory of your computer.

4.	Click “Next”. On this screen, you can create a new virtual hard disk. A virtual HD is simply a large file that will remain on your file system, which will function as if it were an HD for the virtual machine system. Click “Create” button.

5.	On the next screen, you can choose the file format of this new disc. I left the native format of Virtual Box, the VDI and click “Next” button.

6.	In this screen you can choose between two options:
•	Dynamically allocated: In this option, the virtual disk file will only increase in size when new files are written. This means that if you create a 20 Gigabyte disk, but the OS installation and the other files take up only 1 Gigabytes, then the file will only have 1 Gigabytes. The disk will grow in size as it reaches the 20 gigabytes limit.
•	Fixed size: In this option, a 20 Gigabyte virtual disk will occupy this whole size on your real disk.
In order to save more space, I left the first option selected.

7.	Under "Location and file size", enter the name of the file to be created (Ubuntu), and then select the maximum file size (10 gigabytes). To confirm everything and create the disk, click the "Create" button”.

8.	Back in the main Virtual Box window, click on the new virtual machine created and then on the "Settings" button and then on the "Storage" item.

9.	Inside "Storage", Click the "Empty" item that is below the optical disc controller (CD / DVD icon). Once this is done, click the arrow next to the "Optical Drive" field. In the menu that appears, click on the "Select Virtual Optical Disc File" option to use an ISO image. You will then be presented with a screen where you should inform where the ISO image is, select and then click the "Open" button.

Finally, the virtual machine was created and configured.

## **Configuration and deployment of the Ubunto server**

Running the virtual machine, the Ubuntu install file will boot up. Continue through the setup selecting the appropriate settings. After setup has been configured, enter the hostname which I picked the name "Web-server".

Follow the instructions on the screen to setup the username and password. Take notes of both. 
Choose a guided partition and the volume of the entire disk. Confirm changes to the disk in the subsequent menus and installation should start. The machine should reboot when finished.

When it restarts, it prompts you for the login details. After successfully logged in, take a snapshot to save all configuration that has been done.

The Ubuntu Server is now installed.

## **Configuring and Deploying Apache 2**

1.	Before starting the installation of Apache2, check if there is an update using:
(All commands with "sudo" are run with root privileges.)

	Sudo apt-get update
    
And then install Apache2 using:

	Sudo apt-get install apache2
    
2.	Changing the setting to the apache 2 start up at system boot. It'll run automatically  when the virtual machine gets on.

	sudo systemctl enable apache2
  
Now, starting the Apache 2

	sudo systemctl start apache2
    
3.	To verify that everything went as planned, enter the public IP address of the server (localhost) in the browser. The default apache page should appear.

## **Configuring and Deploying MySQL**

1.	To install MySQL database server enter the following command:

	sudo apt-get install mysql-server
    
2.	During installation, the server will ask to select and confirm the password for the "root" MySQL user. Make notes of both.

3.	Run a simple security script that removes some dangerous patterns and slightly block access to our database system.

	sudo mysql_secure_installation
    
Must be pressed "Y" and / or pressed the "Enter" key for each prompt. This will remove some anonymous users and the test database, disable remote root logins, and load these new rules so that MySQL immediately respects the changes that have been made.

The database system is now configured

## **Configuring and Deploying PHP**

1.	Use the following command to install PHP:

	sudo apt-get install php7.0 php7.0-mysql libapache2-mod-php7.0 php7.0-cli php7.0-cgi php7.0-gd
    
2.	Delete the index.html file at the the directory “/var/www/html” (using cd command to get there) so that Apache will first read index.php file instead.

3.	Type the command the following command to test that PHP is working:

	sudo vi /var/www/html/info.php
    
4.	Then press "i" key to allow editing the file. Then enter the code:

	<?php
    
	phpinfo();
    
	?>
    
5.	Press “ESC” and “:wq” to save it.

6.	Open the web browser and type “localhost/info.php”. A page containing configuration information must be showed.

PHP is finalized.

## **Configuring and Deploying Wordpress**

1.	To get started, log into the MySQL root (administrative) account by issuing this command:

	mysql -u root -p
    
2.	After logged in, create a separate database that WordPress can control using the following command:

	CREATE DATABASE wordpress;
    
3.	To create a separate MySQL user account that is used exclusively to operate on the new database. This is the command:

	CREATE USER matheuswpress@localhost IDENTIFIED BY 'password';
    
4.	Granting the user account access to the new database with this command:

	GRANT ALL PRIVILEGES ON wordpress.* TO matheuswpress@localhost;
    
5.	Following the next step:

	FLUSH PRIVILEGES;
    
	Exit
    
6.	Back to the regular command prompt, get wordpress downloaded by using:

	wget -c http://wordpress.org/latest.tar.gz
    
7.	Extracting the files to rebuild the WordPress directory:

	tar xzvf latest.tar.gz
    
8.	Moving the wordpress unpacked:

	cd ~/wordpress
    
9.	copy it to the default configuration file location to get WordPress to recognize the file:

	cp wp-config-sample.php wp-config.php
    
10.	Open it in a text editor:

	nano wp-config.php
    
11.	Change the parameters with the information for the database created:

	/** The name of the database for WordPress **/
    
	define('DB_NAME', 'wordpress');
    
	/** MySQL database username **/
    
	define('DB_USER', 'wordpressuser');
    
	/** MySQL database password **/
    
	define('DB_PASSWORD', 'password');
    
12.	Save and close the file.

13.	Transfer the WordPress files into Apache's document root by typing:

	sudo rsync -av wordpress/* /var/www/html/ 
    
14.	Giving ownership of the word files to the web server (called www-data) :

	sudo chown -R www-data:www-data /var/www/html
    
15.	Changing permissions to allow anyone to read and execute the file:

	sudo chmod -R 755 /var/www/html
    
## **Configure the wordpress site**

1.	Restart the web server and MySQL service to allow changes to take affect:

	sudo systemctl restart apache2.service
	sudo systemctl restart mysql.service
    
2.	Go to the address http://localhost:80/wp-config.php . In case it doesn’t work type:

	Ctrl+F5
    
3.	WordPress initial configuration page Will be shown.

4.	Create an initial administrator account. Take notes of it.

5.	WordPress will confirm the installation, and then ask to log in. Hit the button at the bottom and then fill out the account information.

The WordPress interface will be presented and can be modificate as wish.

## **Conclusion**

The project provides a practical overview that the lessons can not. All goals were met despite some minor problems. In order to avoid some of the problems, some observations will be added.
**Obs1** - Before any installation, make a backup system (snapshot). If something goes wrong, the system can get back to previous settings and not be compromised with the error.
**Obs2** - Make notes of all users and passwords created. This can save you lots of troubles. (Make notes of everything basically).
