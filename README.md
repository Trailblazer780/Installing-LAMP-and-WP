# Installing-LAMP-and-WordPress
This is documentation of installing a LAMP server and deploying WordPress made by Ethan Farrell
For this documentation we are using Ubuntu 18.04 Server on an EC2 AWS instance.

# Table of Contents:
1. [Installing LAMP Stack](#Installing-LAMP-Stack)
2. [Setting up the Database](#Setting-up-the-Database)
3. [Downloading WordPress](#Downloading-WordPress)
4. [Setting up WordPress](#Setting-up-WordPress)
5. [Configuring Apache](#Configuring-Apache)
6. [Enabling the website on Apache](#Enabling-the-website-on-Apache)
7. [Add Entry to Hosts File](#Add-Entry-to-Hosts-File)
8. [Configuring WordPress](#Configuring-WordPress)
9. [Creating A DNS Record in AWS](#Creating-A-DNS-Record-in-AWS)
10. [Completion](#Completion)


## Installing LAMP Stack

To Install the LAMP stack on Ubuntu you need to run this command below. This command will grab, download, and install all of what is needed to run the LAMP server. Once the installation of all of these is completed you can now move on to the next step of the process of configuring the LAMP server.

`sudo apt install apache2 mysql-server mysql-client php7.4 php7.4-dev php7.4-mysql`

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%201%20Installing%20the%20Lamp%20Stack.PNG)

## Setting up the Database

The first thing you need to do to set up the database for the lamp server is to run this command: `sudo mysql` so that you can start to configuring things in the database. The below screenshot will show what it should look like if you have accessed the database properly.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%202%20Setting%20Up%20the%20database.PNG)

First we will need to create a user that the database is going to use. To do this run the following command:
`CREATE USER 'wordpress'@'localhost' IDENTIFIED BY 'Password123.';`

If the command was run correctly it should look like the screenshot below. Remember that for the user `wordpress` can be substituted with whatever you want in the command. The password can also be substituted with whatever you would like but if this is going to be a publicly accessible server you are going to want a more complex password than what I have used in the example.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%203%20Create%20Database%20user.PNG)

Now that we have created a user that can manage the databases we can now create the database that you are going to use with WordPress later on with this documentation you need to run the following command: 
`CREATE DATABASE wordpressDB;`

If you created the database correctly your terminal should now look like the following screenshot below:

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%204%20Creating%20Database.PNG)

To make sure that the database was created successfully run the following command:
`SHOW DATABASES;`

Your terminal should look like the screenshot below and you should see the database you created in the table.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%205%20Show%20Databases.PNG)

After the database has been created we can now go and give the user that we created in the earlier step full access to the database that we have just created. To do this run the following command:
`GRANT ALL PRIVILEGES ON *.* TO 'wordpress'@'localhost';`

If the command was run successfully your terminal should look the screenshot below.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%206%20Grant%20permissions%20to%20DB%20User.PNG)

Now that we have completed the setup of the database and its user we can now go back to our regular terminal and to do this you simply need to run the command: `exit` and you will be brought back to your Ubuntu terminal.


## Downloading WordPress

The first thing we want to do when getting WordPress is to get the latest version. This link is the download link for the latest version of WordPress: `https://wordpress.org/latest.tar.gz`

After we have that link we can now download WordPress onto our Ubuntu machine via the command line. You will want to be inside of your home directory when you are downloading WordPress. The command that you need to run is: `wget https://wordpress.org/latest.tar.gz` If it downloaded correctly your terminal should look like the screenshot below:

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%207%20Downloading%20Wordpress.PNG)

To check and make sure that the file is there you can preform a long listing of your home directory by simply running the `ll` command. The screenshot below is what should be in your home directory if it downloaded properly.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%208%20Checking%20that%20wordpress%20is%20there.PNG)


## Setting up WordPress

The first thing we need to do to setup WordPress is to create a directory that we can put it in. To do this you can run the following command (You can replace the `ethan.nscctruro.ca` with whatever you would like to call your website):

`sudo mkdir /var/www/html/ethan.nscctruro.ca`

After running that command we can now extract the WordPress files from the latest.tar.gz file. To do this run the following command:
`sudo tar -xvzf latest.tar.gz`

When it is done extracting you can perform a long listing on your home directory and you will now see that WordPress has been extracted. To do this run the following command: `ll`

Your terminal should look like the screenshot below and you should see a WordPress directory.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%209%20Extracted%20wordpress.PNG)

The next step is to move all of the contents inside off that wordpress folder to where you website file is located in the Ubuntu system. To do this run the following command(if you called your directory something else you need to replace the `ethan.nscctruro.ca` with whatever you named the directory):

`sudo mv wordpress/* /var/www/html/ethan.nscctruro.ca/`

To confirm that the files moved to that directory properly we can now switch to that directory by running the following command:

`cd /var/www/html/ethan.nscctruro.ca`

Once you have switched the that directory we can now perform a long listing of that directory by running the `ll` command. The screenshot below is what it should look like if all of the files moved to the directory properly.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%2010%20Checking%20wordpress%20moved%20files.PNG)


## Configuring Apache

Now that we have WordPress installed and it is in the website directory the next step we need to take is going to be to setup the Apache configuration so that the website is accessible. First we need to make a copy of the default configuration file to use to setup the website. To do this run the following command:

`sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/ethan.nscctruro.ca.conf`

The next step is to edit the copy we just made and put in our configuration settings for the website. To do this run the following command to edit this configuration: 

`sudo nano /etc/apache2/sites-available/ethan.nscctruro.ca.conf`

The screenshot below shows what it should look like when you first open the configuration file with the command that was used above.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%2011%20Configuring%20apache.PNG)

To configure it we just need to change two things in the configuration file. The first one being the `ServerName` which we will set to whatever we called our website. The second thing being the `DocumentRoot` which will be the directory that our website is located in. The screenshot below will show what the configuration should look like after being configured.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%2012%20After%20Configuration.PNG)


## Enabling the website on Apache

Now that we have configured the host file for the website we can now enable the website so that it is accessible. To do this we need to run the following command:

`sudo a2ensite ethan.nscctruro.ca.conf`

Once that command has been run we now need to restart Apache for the changes to take effect. To do this we need to run the following command: 

`sudo service apache2 restart`

To confirm that Apache is up and running again we need to run the following command: 

`sudo service apache2 status`


## Add Entry to Hosts File

We need to add an entry to the hosts file on our windows machine so that we can access this website that we have just created and configured to setup the WordPress. The hosts file on a windows machine can be found in this location" `C:\Windows\System32\drivers\etc` You will need to open the hosts file with a text editor that has admin permission so that you can make changes to this file. For this example i am going to be using notepad. If you are doing this on a local machine you are going to want the IP to be 127.0.0.1 if you are doing this with a live version the IP is going to be the publicly accessible IP address. In my example I am using my publicly accessible IP address. The below screenshot is what your entry in the hosts file should look like.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%2013%20hosts%20file%20entry.PNG)


## Configuring WordPress

The first thing that we need to do when configuring WordPress is going to be changing the owner of the directory that we made in earlier steps for the website so that WordPress can be able to write to files inside of that directory. The easiest way to do this is going to be to run this command that will change the owner of the directory: `sudo chown -R www-data:www-data /var/www/html/ethan.nscctruro.ca`

Now that the permissions are okay and we will not run into any issues we can now access our website via the link that we named it in the config file for Apache. In this case the link for this example is ethan.nscctruro.ca and when I access the website in a web browser the following page should come up.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%2014%20initializing%20wordpress.PNG)

After clicking the "Let's Go" button you will be brought to a page that you need to fill out so that WordPress can have access to the database we created earlier. You are going to need to provide the name of the database, the username you made for the database and the password associated with that username, since the database and the Apache server are running on the same machine we can leave the database host as localhost, and finally we need to make a table prefix for the database which can be anything you want it to be but its best to keep it short and simple. The below screenshot is what it should look like when you have filled in all of the information.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%2015%20Wordpress%20configuration%20.PNG)

After all of that information has been entered in there correctly we can now click the "Submit" button and you will be brought to a page that looks like this and all you need to do is click the "Run the installation" button.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%2016%20Wordpress%20final%20installation.PNG)

Once you run the installation you will be brought to a page that you need to fill out for your admin account on the WordPress website. The page will look like the screenshot below and all you need to do is fill in the required information. Once the required information is filled out click the "Install WordPress" button.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%2017%20Wordpress%20admin%20account.PNG)

You will then be brought to a page that looks like the screenshot below and you just need to log in with the username and password you provided in the previous step.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%2018%20Wordpress%20installed.PNG)

If you have been successful at logging into the new WordPress website you will now be brought to you main dashboard for the website and it should look like the screenshot provided below.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%2019%20Wordpress%20Dashboard.PNG)


## Creating A DNS Record in AWS

Now that you have successfully created and deployed a publicly accessible WordPress website using an EC2 instance from AWS it is now time for the final step, creating a DNS record using an AWS service called Route 53.

Once you are in the Route 53 service that is provided by AWS it should look like the screenshot below and all you need to do is click on the "Create Record" button and you will be brought to a new page where you can create the actual DNS record.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%2020%20Creating%20DNS%20Record.PNG)

Once you are on the Quick Create Record menu it is very simple to fill out. First we need to fill out the prefix of the website which in this case for my example is ethan2. The next step is to select the record type and for this example we will be using a type A record with an IPV4 address because my publicly accessible IP address is an IPV4 address. If you have an IPV6 publicly accessible address then you would select the type A record for IPV6 address'. Finally you just need to input your publicly accessible IP address whether it is IPV4 or IPV6 and click the "Create Records" button. Now that you have created this record you can remove the entry that you had put in your hosts file on your windows machine and you can now access your website from any modern browser. Note that it may take up to 48 hours for the DNS record to become active depending on which DNS servers your machine uses. The below screenshot is what you record should look like.

![alt text](https://github.com/Trailblazer780/Installing-LAMP-and-WP/blob/main/Images/Capture%2021%20Record%20Creation.PNG)


## Completion

Congratulations, you have now completed setting up a publicly accessible WordPress website on an AWS EC2 instance.



