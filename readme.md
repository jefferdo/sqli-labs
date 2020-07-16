# SQLI LABS

# Introduction

SQLI-LABS is a platform to learn SQLI Following labs are covered for GET and POST scenarios:

You can refer to the original repository from this link: [https://github.com/Audi-1/sqli-labs](https://github.com/Audi-1/sqli-labs)

The original source code is not compatible with the latest PHP version. Therefore, you must use PHP 5. Or you can use SQLI Converter to modify the code to work with latest PHP. MySQLConverterTool by Philip is a good Opensource project designed to do this specific task. You can refer to this link to know about it more and convert the code to be compatible with php7+: [https://github.com/philip/MySQLConverterTool](https://github.com/philip/MySQLConverterTool)

Or just clone [https://github.com/jefferdo/sqli-labs](https://github.com/jefferdo/sqli-labs) which i have converted to be compatible and tested.

# Configuration

To run the SQLI LABS you should configure a webserver with latest Apache, PHP, and MySQL. I always recommend using a fresh copy of Linux VM for best results. Or you can just use an existing webserver. I am using these versions of above-mentioned services

- Ubuntu 18.04.2 LTS
- Apache 2.4.29
- PHP 7.2.24
- MySQL 5.7.30

## Installing Apache

Install Apache using Ubuntu&#39;s package manager, _apt_:

- _sudo apt update_
- _sudo apt install apache2 -y_

_Additionally, you can configure the Firewall to accept apache traffic,_

- _sudo ufw app info &quot;Apache Full&quot;_

_You can do a spot check right away to verify that everything went as planned by visiting your server&#39;s public IP address in your web browser._

## Installing MySQL

Again, use apt to acquire and install this software:

- _sudo apt install mysql-server -y_

When the installation is complete, run a simple security script that comes pre-installed with MySQL which will remove some dangerous defaults and lock down access to your database system. Start the interactive script by running:

- _sudo mysql\_secure\_installation_

This will ask if you want to configure the VALIDATE PASSWORD PLUGIN, Answer Y for yes, or anything else to continue without enabling. In our case, I am recommending keeping it without enabling it. If you answer &quot;yes&quot;, you will be asked to select a level of password validation. Keep in mind that if you enter 2 for the strongest level, you will receive errors when attempting to set any password which does not contain numbers, upper and lowercase letters, and special characters, or which is based on common dictionary words.

Regardless of whether you chose to set up the VALIDATE PASSWORD PLUGIN, your server will next ask you to select and confirm a password for the MySQL root user. This is an administrative account in MySQL that has increased privileges. Think of it as being like the root account for the server itself (although the one you are configuring now is a MySQL-specific account). Make sure this is a strong, unique password, and do not leave it blank.

If you enabled password validation, you will be shown the password strength for the root password you just entered, and your server will ask if you want to change that password. If you are happy with your current password, enter N for &quot;no&quot; at the prompt

For the rest of the questions, press Y and hit the ENTER key at each prompt. This will remove some anonymous users and the test database, disable remote root logins, and load these new rules so that MySQL immediately respects the changes you have made.

Note that in Ubuntu systems running MySQL 5.7 (and later versions), the root MySQL user is set to authenticate using the **auth\_socket** plugin by default rather than with a password. This allows for some greater security and usability in many cases, but it can also complicate things when you need to allow an external program (e.g., phpMyAdmin) to access the user.

If you prefer to use a password when connecting to MySQL as root, you will need to switch its authentication method from **auth\_socket** to **mysql\_native\_password**. To do this, open the MySQL prompt from your terminal:

- _sudo mysql_

_Next, check which authentication method each of your MySQL user accounts use with the following command:_

_mysql\&gt; SELECT user, authentication\_string, plugin, host FROM mysql.user;_

Output

+------------------+-------------------------------------------+-----------------------+-----------+

| user | authentication\_string | plugin | host |

+------------------+-------------------------------------------+-----------------------+-----------+

| root | | auth\_socket | localhost |

| mysql.session | \*THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql\_native\_password | localhost |

| mysql.sys | \*THISISNOTAVALIDPASSWORDTHATCANBEUSEDHERE | mysql\_native\_password | localhost |

| debian-sys-maint | \*CC744277A401A7D25BE1CA89AFF17BF607F876FF | mysql\_native\_password | localhost |

+------------------+-------------------------------------------+-----------------------+-----------+

4 rows in set (0.00 sec)

In this example, you can see that the  **root**  user does in fact authenticate using the auth\_socket plugin. To configure the  **root**  account to authenticate with a password, run the following ALTER USER command.

_mysql\&gt; ALTER USER &#39;root&#39;@&#39;localhost&#39; IDENTIFIED WITH mysql\_native\_password BY &#39;password&#39;;_

Then, run FLUSH PRIVILEGES which tells the server to reload the grant tables and put your new changes into effect:

_mysql\&gt; FLUSH PRIVILEGES;_

_At this point, your database system is now set up and you can move on to installing PHP, the final component of the LAMP stack._

## Installing PHP

Once again, leverage the apt system to install PHP. In addition, include some helper packages this time so that PHP code can run under the Apache server and talk to your MySQL database:

- _sudo apt install php libapache2-mod-php php-mysql_

_At this point all services are ready to use for SQLI Labs. If you need more info, refer to this link:_

[https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-ubuntu-18-04#conclusion](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-ubuntu-18-04#conclusion)

Clone the SQLI LABS using:

- _git clone [https://github.com/jefferdo/sqli-labs](https://github.com/jefferdo/sqli-labs)_

_and copy the folder into /var/www/html/ directory using_

- _cp ./sqli-labs /var/www/html/_

_then navigate to /var/www/html/sqli-labs/sql-connections_

- _cd /var/www/html/sqli-labs/sql-connections_

_and open_ _db-creds.inc_ _file using your favourite text editor, and update your credentials_

![](RackMultipart20200716-4-t941d_html_6ad5c579729934a8.png)

_You may have to create a new user for this application on mysql, it easy as,_

- _sudo mysql_

_mysql\&gt; CREATE USER &#39;ubuntu&#39;@&#39;localhost&#39; IDENTIFIED BY &#39;Abc@1234&#39;;_

_mysql\&gt; GRANT ALL PRIVILEGES ON \*.\* TO &#39;ubuntu&#39;@&#39;localhost&#39;;_

_now navigating to http://\&lt;your-ip-address\&gt;/sqli-labs/index.html on your browser will open the sqli-labs environment._
