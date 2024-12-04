ONT is giving us data via globus
### install globus client in a separate environment 

```
python3.8 -m venv globus_env
source globus_env/bin/activate
pip install globus_cli

globus --help
globus login
#follow instructions on screen
```

### Check what is in the collection with ID shared with us by mail, should see our files
```
globus gcs collection show 026db892-c778-45f9-b5ae-a0383e073714
```
Need to define endpoints, at the beginning, they are empty
```
globus endpoint search --filter-scope my-endpoints
#if there is something to show you can look at it
globus endpoint show <ID>
```

Use globus client to define an endpoint:
```
 cd /data/hestia/rkabiljo/globusconnectpersonal-3.2.6/
./globusconnectpersonal -setup
#follow instructions on screen.  Give a name for endpoint.  you will get an ID
```
In order for it to work, two things need to be set up manually:
```
cd ~/.globusonline/lta/
nano config-path
```
in that file paste the ID you got when you set up the endpoint
```
nano config-paths 
```
This should look like this:
```
~/,0,1
/data/hestia/rkabiljo/ONT/,0,1
```
this enables it to write to local directories that are listed here.  Paste your target directory here in exactly this format
```
./globusconnectpersonal -start &
```
To restart it use 
```
./globusconnectpersonal -stop
./globusconnectpersonal -start &
```

To transfer data:
```
globus transfer --recursive 026db892-c778-45f9-b5ae-a0383e073714:/C ebaac63a-ad83-11ef-9c5d-774ae94090b7:/data/hestia/rkabiljo/ONT/C/
```
the first long string is collection ID
then as target, we have the endpoint id (ebaac63a-ad83-11ef-9c5d-774ae94090b7) and target directory, that should be in config-paths file. I did it sample by sample, but initiated many samples simultaneously.

### to monitor the transfer:
```
globus task list
globus task show TASK_ID
#to cancel it
globus task cancel TASK_ID 
```

