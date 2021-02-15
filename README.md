# PostgreSQL 13 installation_ubuntu

[LINUX] GUIDE FOR UBUNTU USERS (tested on 20.04)

I've had some difficulties but finally managed to install PostgreSQL and restore the database.

Here's how I've done:

______________________________

## POSTGRESQL 12 INSTALLATION

1. Open the terminal and run these four commands to install PostgreSQL 12

`sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

sudo apt-get update

sudo apt-get install postgresql-12`

2. Enable PostgreSQL service:

`sudo systemctl enable postgresql.service`

3. Update the UNIX password (and REMEMBER IT):

`sudo passwd postgres`

You'll be asked to enter the password twice. Do it.

4. Access PostgreSQL shell and set the password for the DB administrator:

`sudo su -l postgres`

Enter your sudo password. Then to enter the psql shell type:

`psql`

Once here you have to set the password for the DB administrator (and REMEMBER IT):

`postgres=# \password postgres`

Once you've set the password, quit and exit by running these two commands:

`\q

exit`



______________________________

## PGADMIN4 INSTALLATION

1. If curl is not installed in your system, install it:

`sudo apt-get install curl`

2. Run these three commands to install pgAdmin4:

`curl https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo apt-key add

sudo sh -c 'echo "deb https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'

sudo apt install pgadmin4`

3. Reboot your system.



______________________________

## CREATE A SERVER CONNECTION

1. Open pgAdmin 4 from your application menu.

2. You'll be asked to choose a password. Type that in (and REMEMBER IT).

3. Click on Add New Server at the center of the page.

4. In the General tab, choose a name for your server (e.g. PostgreSQL 12).

5. In the Connection tab, fill the Hostname/address field with the first part of the URL you see in your browser address bar, before the column. It should be something similar to 127.0.0.1

6. In the Connection tab, fill the Password field with the DB administrator password you chose before. Check the Save password? option and then click on Save.



______________________________

## RESTORE THE DATABASE

1. Open your server, right click Databases and then Create -> Database...

2. Fill the Database field with dvdrental.

3. Click on Save.

4. Right click on your newly created dvdrental database and select Restore...

5. Under Filename, click on the three dots button and navigate to the location where you downloaded the dvdrental.tar file. If the file doesn't show up, select All Files from the dropdown menu in the bottom right corner.

6. In the Restore options tab, enable Pre-data, Post-data and Data, then click Restore.

7. Right click on dvdrental database and select Refresh...

8. Right click on dvdrental database and select Query Tool...

9. Try to run this query to check if the database was restored correctly:

SELECT * FROM film;
