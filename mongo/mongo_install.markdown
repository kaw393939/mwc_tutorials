Installing MongoDB for Ubuntu Linux 12.04
MongoDB Introduction & Brief History
MongoDB (from “humongous”) is an open source document-oriented database system, and the leading NoSQL database solution written in C++, that has features of being agile and scalable. Let’s have a brief history of knowing what MongoDB is. MongoDB is developed and supported by 10gen. 10gen began the development of MongoDB in October 2007. 
10gen was founded in 2007 by former DoubleClick founder and CTO Dwight Merriman and former DoubleClick CEO and Gilt Groupe founder Kevin P. Ryan with former Doubleclick engineer and ShopWiki founder and CTO Eliot Horowitz. The company originally aimed to build a platform as a service similar to Google App Engine. In 2009, the company decided to open source the database component, MongoDB as a stand-alone product with an AGPL license. In March 2010, from version 1.4, MongoDB has been considered production ready. 
According to Eliot Horowitz, 10gen CTO and Co-founder,
“MongoDB wasn’t designed in a lab. We built MongoDB from our own experiences building large scale, high availability, robust systems. We didn’t start from scratch, we really tried to figure out what was broken, and tackle that. So the way I think about MongoDB is that if you take MySql, and change the data model from relational to document based, you get a lot of great features: embedded docs for speed, manageability, agile development with schema-less databases, easier horizontal scalability because joins aren’t as important. There are lots of things that work great in relational databases: indexes, dynamic queries and updates to name a few, and we haven’t changed much there. For example, the way you design your indexes in MongoDB should be exactly the way you do it in MySql or Oracle, you just have the option of indexing an embedded field.”

An overview of MongoDB is that it focuses on flexibility, power, speed and ease of use. 
MongoDB stores data in JSON documents (serialized to BSON). This JSON document provides rich data model and dynamic schema making it easier to evolve the data model than with a Relational Database Management System. However, MongoDB still provides a lot of features of the classical RDBMS for most purposes. By keeping related data together in documents, queries can be much faster than in a relational database where data is separated in multiple tables and needs to be joined, Unlike in MongoDB it allows NoSQL functionalities so you don’t have to join tables anymore. Another good characteristic of MongoDB is autosharding which allows you to scale your cluster by adding more machines, increasing the capacity without any downtime. 

	Installation Note: 
MongoDB is a server process that can run on Linux, Windows and OS X. It can be run both as a 32-bit or 64-bit application. But it is recommended running in 64-bit mode, since MongoDB is limited to a total size of 2GB for all databases in 32-bit mode. 
The MongoDB process listens on port 27107 by default and MongoDB stores its data in files (the default location is /data/db) 

MongoDB Installation: 
First, you need to be in admin mode which will provide more privileges in the installation process than just in a normal user mode to save you from problems by executing on the command line: 

	$ sudo su - 
Press {Enter} and you must provide your password for the admin of your Linux computer. 
Then configure the package for MongoDB. In your GNU terminal, type the following command: 

	$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10
The ‘apt-key’ call registers the public key of the custom 10gen MongoDB aptitude repository. 
The custom 10gen repository list file is created containing the location of the MongoDB repository that will be downloaded by typing this in the command line:
 
	$ echo "deb http://downloads-distro.mongodb.org/repo/ubuntu-upstart dist 10gen"
It will download the packages needed for installation of your MongoDB. You should see something similar to the image below: 
Once its done downloading the packages, you can start the installing process by typing: 

	$ sudo apt-get update && sudo apt-get install -V mongodb-10gen
This will update aptitude for packages and then eventually aptitude is told to install MongoDB.
The accompanying picture here will give you an idea how it looks while installing and finished installing MongoDB. 

Once it is done installing MongoDB, you can issue the command below just to properly start MongoDB or make sure it is already started before trying it: 

	$ sudo service mongodb start
You can try running MongoDB by entering this command: 

	$ mongo
This command invokes to show the shell command line of MongoDB and you are ready to use it. You should see something like below that it is connecting to test, connected to your localhost by default. Congratulations! You have installed MongoDB in your Ubuntu Linux 12.04! 

 
Now you can try the basic MongoDB shell commands for the database. 
Don’t forget to close MongoDB shell by entering the command on the terminal: 

	$ exit
However, there are some configurations and commands you would like to use and explore your MongoDB database configurations. 

Controlling MongoDB
These are some basic commands controlling your MongoDB that are firsthand important to know. Controlling when to start, stop or restart the process of the database is by commands too.
This is for checking the current status of your MongoDB: 
$ sudo service mongodb status 
This one is for starting MongoDB:
 
     $ sudo service mongodb start
This command is for stopping the database:
 
	$ sudo service mongodb stop
And this one is for restarting MongoDB:
 
	$ sudo service mongodb restart
This image here shows how these MongoDB shell commands are used. Notice the response of the system when issuing the commands controlling MongoDB through those processes.
 

Configure MongoDB
You may want to configure your MongoDB through finding the configuration script and changing it for your preferences, you may take a look at the following:
The control script to start, stop or restart is found in 
	/etc/init/mongodb.conf
	The data file directory is /var/lib/mongodb/
	The logs file directory is /var/log/mongodb/




References used are: 
http://genealo.org/wiki/How_to_install_MongoDB_on_Ubuntu_12.04
http://blog.bravi.org/?p=778
https://www.digitalocean.com/community/articles/how-to-install-mongodb-on-ubuntu-12-04
http://mongojs.org/install-mongodb-ubuntu-11-04-natty
http://serverfault.com/questions/408350/mongodb-installation-in-ubuntu-12-04
http://en.wikipedia.org/wiki/10gen
http://www.mongodb.org/about/introduction/

Tutorial done by: Ralph
