# Python Pyramid Basic Scaffold + Advanced testing

## Setup

Install the pyramid package:

```
sudo pip3 install pyramid
```

Check packages to make sure it has installed correctly:

```
sudo pip3 freeze --local
```

Create a basic scaffold in a directory of your choice:

```
pcreate -s starter test_scafold
```

Install (run as sudo if using container or virtual IDE - cloud9 etc.):

```
python3 setup.py develop
```

Test that the application starts:

```
pserve development.ini
```

After running the above, you can test access using the provided url. 
If, like me, you are using a virtual IDE environment (I am using Cloud9 on AWS) you are going to need to do some extra configuration to get this up and running. 
Open the EC2 console, and allow traffic for the instance on the port provided: 6543.
Go back to your application, and add the DNS url of the instance to the listen value in the development.ini file. 
Mine looks like this, dont forget to append the port to the url!

```
[server:main]
use = egg:waitress#main
listen = xxx-x-x-xxx-xx.ap-southeast-1.compute.amazonaws.com:6543

```

If you have followed the above, paste the url into your browser and hit enter, you should get the following templated page:

![starter_scaffold](https://s3-ap-southeast-1.amazonaws.com/python-pyramid/pyramid_starter_scaffold.PNG)