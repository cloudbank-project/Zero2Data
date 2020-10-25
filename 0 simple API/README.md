# 0 simple API

## Overview

Suppose we have an "on all the time" EC2 hosting a web service. We'd like multiple Clients to be able to 
ping this service in a more-or-less continuous manner. We'll use the Python web framework called `bottle`
as it is one of the simplest available. 


## Tutorial


* Install Anaconda
    * Search `install Anaconda Linux` and follow the instructions
    * Shortcut: Figure out the down path and use `wget` to download the installer on the VM
        * For example: `wget https://repo.anaconda.com/archive/Anaconda3-2020.07-Linux-x86_64.sh`
        * `bash Anaconda3-2020.07-Linux-x86_64.sh` and follow the prompts
    * On Ubuntu I installed Anaconda in the /home/ubuntu directory and needed to add the path for conda
        * `export PATH=~/anaconda3/bin:$PATH`


* Install `bottle`, a lightweight Python web server
    * `pip install bottle`
    

Working from [this link](https://bottlepy.org/docs/dev/tutorial.html) at the moment. 
