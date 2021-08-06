# Rails-app-in-a-Vagrant-box

#Author: Sailesh Khadka

#Date: 08/06/2021 11:18:59 pm 

Simple web application built with the Ruby on Rails web framework in a Vagrant box.
Configure and run image for Vagrant

.	Install hashicorp Vagrant for your respective OS.

.	Install Virtual Machine.

.	Configure Vagrant box
- Use hashicorp/bionic64 vagrant box because this application was tested with this image.


Run vagrant:
- vagrant init and vagrant up
-vagrant provision
- vagrant ssh
After that you are logged on to the virtual machine.
To run Ruby application you have to install the respective version of ruby and rails and postgresql database.

Requirements:

	System must be updated i.e. sudo apt-get update

	Install rvm or rbenv version manager to install ruby

	Ruby version -2.4.1

	Postgresql database

	Rails

	Gem file to run the application i.e. we can get it form bundle install

	Curl  => \curl -sSL https://get.rvm.io | bash -s stable

	Gpg2  =>  sudo apt-get install gnugp2

Problem faced during configuration

•	The most common problem is versioning issue when running ruby and some gem package, i.e. system didn’t identify bundle package version according to project.

•	When doing bundle install in project directory make sure first delete/remove Gemfile.lock and then run bundle install. [because gemfile.lock already contains package name which didn’t support in your project].

•	Some of the gem file didn’t install when doing bundle install  so, we have to install them manually like,
[An error occurred while installing pg (0.21.0), and Bundler cannot continue.
Make sure that `gem install pg -v '0.21.0' --source 'https://rubygems.org/'` succeeds before bundling.] In this case, we have to install manually i.e. gem install pg -v '0.21.0' --source 'https://rubygems.org/'

After all the issues were resolved finally, we were moving head towards creating database. 
As we are using postgesql I have faced so many problems during setup database.

•	First when creating role with password for Postgresql database,
su - postgres
[error: No passwd entry for user 'postgres']

After some googling I found the solution here and needs to restart postgres service sudo service postgresql restart

•	Then I need to give the admin privilege to user ‘postgres’ for the respective database.

•	Then edit database.yml file, define your own database and user pwd here, for eg please see the attached image.
 
Note: Make sure you update your repository list. 

OR, 

Enable the PostgreSQL apt repository

Create the file “/etc/apt/sources.list.d/pgdg.list” and add the corresponding line for the repository in it:
vagrant@vagrant:~/Rails-app-in-a-Vagrant-box :~# sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ bionic-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'

Import the repository signing key and update the package lists:
vagrant@vagrant:~# wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add – 

Then update your repository list i.e., 
sudo apt-get update

Boom :D you can connect to PostgreSQL

Now you can login to your cluster 
vagrant@vagrant:~# ps -ef | grep postgres


The most important part is make sure you forward port in vagrantfile because to run the hosted app in rails server you have to run from host machine.

 
When done you can run your rails server, 
rails s -b domainname
 

Finally, a simple web is hosted using rails server 

**YOU CAN FIND DEMO_IMG IN **

Rails-app-in-a-Vagrant-box/demogif/


