## 
Get the list of apps and delete them
```Shell
doctl apps list --format ID | xargs -I {} bash -c "if [[ '{}' != ID ]]; then doctl apps delete -f {}; fi"
```
## 
Contexts : create access token from Digital Ocean console which has to be provided as part of init
```Shell
doctl auth init --context <name>
doctl auth list
doctl auth switch --context <name from list> 
```

##
Apps
```Shell
doctl apps create --spec <spec file path>
doctl apps get <app id> -o json |grep phase
doctl apps delete <app id> -f 
```
##
Droplet
```Shell
doctl compute droplet list --format ID --no-header | xargs doctl compute droplet delete -f -t <access token>
```
