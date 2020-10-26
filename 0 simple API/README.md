# 0 simple API

## Overview

Suppose we have an "on all the time" EC2 hosting a web service. We'd like multiple Clients to be able to 
ping this service in a more-or-less continuous manner. We'll use the Python web framework called `bottle`
as it is one of the simplest available. 


## Tutorial

* Start an EC2 instance (with keypair file in hand): Typically free tier, like a T2 micro.
* Log in to this instance.


* If you use the `vim` text editor and are not fond of multi-colored font...
    * Edit / create the file `~/.vimrc` and append the line `syntax off`. 
 

* Install Anaconda
    * Search `install Anaconda Linux` and follow the instructions
    * Shortcut: Figure out the down path and use `wget` to download the installer on the VM
        * For example: `wget https://repo.anaconda.com/archive/Anaconda3-2020.07-Linux-x86_64.sh`
        * `bash Anaconda3-2020.07-Linux-x86_64.sh` and follow the prompts
    * On Ubuntu I installed Anaconda in the /home/ubuntu directory and needed to add the path for conda
        * `export PATH=~/anaconda3/bin:$PATH`


* Install `bottle`, a lightweight Python web framework
    * `pip install bottle`
    

Working from [this link](https://bottlepy.org/docs/dev/tutorial.html) at the moment. 



## Bottle server application

This code defines two routes, `hello` and `exchange`. The corresponding URLs would be 

```
http://12.23.34.45:8080/hello
http://12.23.34.45:8080/exchange?task=5
```

The former URL is a simple hello world. 

The latter will build a key-value pair from the inbound qualifiers at the end of the URL, 
specifically from `task=5`. In fact multiple such key-value pairs can be included if they are 
separated by the `&` character in the URL. 


Here is the Client test code: 


```
import requests
import time

tic = time.time(); add_37 = requests.get('http://12.23.34.45:8080/exchange?task=' + str(5)).text; toc = time.time()

print(add_37)
print(1000.*(toc-tic))
```

Here is the corresponding Server code, with remarks to follow. 


```
from bottle import request, route, run, template
import json

@route('/hello')
def hello():
    print('site was hit on route "hello"')
    return 'be swell and have two or three 3.14s'

@route('/exchange', method='GET')
def exchange_numbers():
    print("                  EXCHANGE was hit")
    task_value = request.GET.task.strip()
    print('task_value is', task_value, 'with type', type(task_value))
    task_integer = int(task_value)
    new_integer = task_integer + 37
    print(type(task_integer), task_integer, 'becomes ->', new_integer)
    return str(new_integer)

run(host='0.0.0.0', port=8080, reloader=True)
```


A `{ "task" : "5" }` key-value pair arrives at the server's route-function
`exchange_numbers()` as an HTTP GET. The code 
anticipates the `task` key and assigns the value as a string to `task_value`. This value plus 37 
is returned; so the Client will receive `42`. 
Print statements show the progression on the server side.


The point: Python code runs as a Client on any computer connected to the internet.
The program interacts dynamically with a Server running the Python Bottle web framework.
In our case this Server code runs on an AWS EC2 instance. 
Typical latencies ranged from 5 to 100 milliseconds. Lower latency unsurprisingly
was from another EC2 instance acting as the Client.


