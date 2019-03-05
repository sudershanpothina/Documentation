## get list of all the branches and tags
git rev-list --branches --tags

#### or you can say 

git rev-list --all


## git hooks
trigger something after the code is pushed to the remote server

goto the folder .git/hooks
you can add a shell script to execute on pre-push
make sure it has a chmod of +x 
and also the name has to start with the same as sample (ex pre-push)

works only on local repo

create a file link as follows 
```
ln -s <source path of script at file root location> <targert path .hooks/filename>
```
after the clone run this command


#### This can be done on UI using webhooks
git sends a post message to the url with the complete data
the end point can be a rest service that can be used to process any details

## git reset
```
git reset <commit sha>
git add .
git commit -m "message goes here"
git push origin <branch name>
```
