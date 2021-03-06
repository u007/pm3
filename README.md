# PM3

# Installing PM3

```
wget https://github.com/bluevinegar/pm3/raw/master/bin/pm3
sudo mv pm3 /usr/bin/

```

# start pm3 process in background

You can start the main process in background as the user that you wish to save configuration to $HOME/.pm3/

```
nohup pm3 start &
```
Your pm3 is now daemonized, monitored and kept alive forever.


# Managing Applications

Once applications are started, you can manage them easily.

To list all running applications

```
pm3 list
```

Managing apps is straight forward:

```
pm3 stop <app_name>|'all'|json_conf
pm3 restart <app_name>|'all'
pm3 delete <app_name>|'all'
```

## Example

```
pm3 start app.json
```

app.json

```
{
  "name": "app1",
  "script": "npx",
  "cwd": "/home/ubuntu/app1",
  "args": "babel-node server.js",
  "env": {
    "NODE_ENV": "production"
  }
}
```

To save running process for persisted restart:
```
pm3 save
```

To restore last saved process:

```
pkill pm3
pm3 boot
```

or 

```
pm3 delete all # this will remove all running processes (cannot undo)
pm3 resurrect# loads saved processes
```


## To view logs:

```
pm3 log <app_name> --lines 200
```

for error log

```
pm3 log <app_name> --error
```

# process flow

* bin/pm3.dart send request to socket io on server
* lib/pm_socket.dart received and run command
* lib/pm.dart 

# TODO

* memory limit monitoring and restart

# Known bugs

* TODO

# deploy to system startup

```
# vi /etc/rc.local
cd /home/ubuntu/ && su ubuntu -c 'nohup pm3 start &'
su ubuntu -c 'sleep 3 && pm3 resurrect'
```

or 

```
# vi /etc/rc.local
cd /home/ubuntu && su ubuntu -c 'pm3 boot'


```

# Support

Community Support: 

[https://gitter.im/bvpm3/community#](https://gitter.im/bvpm3/community#)



