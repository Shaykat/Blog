AWS Linux Server configuration with Mongodb Scrapy Python Git

# Create an AWS EC2 free tier Linux Ubuntu 18.x server

There are two types of free Linux machine in AWS. One is Amazon Linux and another one is Amazon Linux 2. I created an instance with 8GB of Storage and 1GB of Memory and created security rules http, https, ssh connection.

# Install MongoDB
I have installed the MongoDB 4.0 Community Edition on Amazon Linux 2 using the yum package manager.
 
To check the Machine version I used this command in the shell

``` grep ^NAME  /etc/*release ```

The result should be Amazon Linux or Amazon Linux AMI. My machine version in amazon linux ami and that's why I get the mongodb version for Amazon Linux 2 and install it.

#Configure the Package Management System (yum)

Create a ```/etc/yum.repos.d/mongodb-org-4.0.repo``` file so that I can install MongoDB directly using yum.


Here is the script for installing mongodb using yum Package Manager. 
```
[mongodb-org-4.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/amazon/2/mongodb-org/4.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.0.asc
```

Then to install the mongodb just run the following command
```sudo yum install -y mongodb-org```

To run the mongodb service on the server run the following command.
```sudo systemctl start mongod```

To verify that MongoDB has started successfully.
```sudo systemctl status mongod```

To stop the mongodb service need to run the following.
```sudo systemctl stop mongod```
 
```Mongod.conf``` file location etc/mongod.conf.

```Mongod.conf``` file does not allow tab in the script. It accept space as indentation.

# Install python, scrapy, git
To install the git I just needed to run the following command if yum package manager.
```yum install git```
 
To install python 3.7 there are some prerequisites like gcc compiler. So first I need to install the gcc compiler using the yum package manager.
```yum install gcc openssl-devel bzip2-devel libffi-devel```
 
Then download the python package using the following commands.
```
cd /opt
sudo wget https://www.python.org/ftp/python/3.7.9/Python-3.7.9.tgz
```
 
To extract the package
```sudo tar xzf Python-3.7.9.tgz```
 
 
Then install the python using the following  commands.
```
cd Python-3.7.9
sudo ./configure --enable-optimizations
sudo make altinstall
```
 
After the installation is completed, remove the tar file from the disk.

```sudo rm /usr/src/Python-3.7.9.tgz```

Now check the python version using the following command.

```python3.7 -V```

After completing the python installation now it is a matter of one command to install scapy on the machine. 

```Pip3.7 install scrapy```


