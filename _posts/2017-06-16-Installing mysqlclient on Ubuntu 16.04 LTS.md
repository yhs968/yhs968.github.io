---
layout: post
title:  "Installing mysqlclient on Ubuntu 16.04 LTS"
date:   2017-06-16
categories: db
---

mysqlclient is a python library to connect to a MySQL DB. However, when you install mysqlclient on ubuntu 16.04 LTS, you may get the following error:

```bash
$ pip install mysqlclient
Collecting mysqlclient
  Using cached mysqlclient-1.3.10.tar.gz
    Complete output from command python setup.py egg_info:
    /bin/sh: 1: mysql_config: not found
    Traceback (most recent call last):
      File "<string>", line 1, in <module>
      File "/tmp/pip-build-58kk7s2k/mysqlclient/setup.py", line 17, in <module>
        metadata, options = get_config()
      File "/tmp/pip-build-58kk7s2k/mysqlclient/setup_posix.py", line 44, in get_config
        libs = mysql_config("libs_r")
      File "/tmp/pip-build-58kk7s2k/mysqlclient/setup_posix.py", line 26, in mysql_config
        raise EnvironmentError("%s not found" % (mysql_config.path,))
    OSError: mysql_config not found

    ----------------------------------------
Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-build-58kk7s2k/mysqlclient/

```
So, the message says that **mysql_config** is not found.

At first glance, I thought that this must be some kind of a configuration file. However, it is actually a *program* for a Unix-based OS's that you need to connect to a MySQL db.
(See [here](https://dev.mysql.com/doc/refman/5.7/en/mysql-config.html) for more details.)

The mysql_config program is provided in the central repository, so you can easily get mysql_config by executing
```bash
$ sudo apt install libmysqlclient-dev
```


Now, you can install mysqlclient without any problem.
```bash
$ pip install mysqlclient
```
