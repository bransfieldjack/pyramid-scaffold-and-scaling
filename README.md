# Python Pyramid Basic Scaffold + Advanced testing

![pyramid](https://s3-ap-southeast-1.amazonaws.com/python-pyramid/pyramid.jpg)

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

## Configuration

The most important file in our scaffold is (no surprises) '__init__.py'.
The file contains the configuration and similarly to Django it uses WSGI. 
The contents look like:

```
from pyramid.config import Configurator


def main(global_config, **settings):
    """ This function returns a Pyramid WSGI application.
    """
    config = Configurator(settings=settings)
    config.include('pyramid_jinja2')
    config.add_static_view('static', 'static', cache_max_age=3600)
    config.add_route('home', '/')
    config.scan()
    return config.make_wsgi_app()

```

## Next up, Views!

Use the following command check which routes have already been defined:

```
proutes development.ini
```

You should have something similer returend:

```
Name                         Pattern                            View                            Method    
----                         -------                            ----                            ------    
__static/                    /static/*subpath                   test_scaffold:static/           *         
home                         /                                  test_scaffold.views.my_view     *         
debugtoolbar                 /_debug_toolbar/*subpath           <unknown>                       *         
__/_debug_toolbar/static/    /_debug_toolbar/static/*subpath    pyramid_debugtoolbar:static/    *      
```

You can also check production.ini:

```
proutes production.ini
```

The result:

```
Name         Pattern             View                           Method    
----         -------             ----                           ------    
__static/    /static/*subpath    test_scaffold:static/          *         
home         /                   test_scaffold.views.my_view    *         
```

Finally, we can check the routes for our views using:

```
pviews development.ini /
```

## How to add a views


