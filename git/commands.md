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
