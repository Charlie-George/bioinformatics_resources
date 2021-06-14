To transfer information from local to remote computer can use an rsync command like: 

```
rsync -rt /path/to/current/location loginname@headnode.address.ox.ac.uk:/path/to/remote/machine
```

This copies timestamp of file and all files in the the folder
NOTE - symbolic links will have pointer copied but not the full file!
