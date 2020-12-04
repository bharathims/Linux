# Github


## Initial Configuration 

* `git config --global user.name 'Bharathi M'`

* `git config --global user.email 'bharathi95@live.com'`

* `git config --global --list` -- Check the info you just provided


## Basic commands

* `git add` -- add file
	- `git add .` -- adds all files
	- `git add file_name` -- adds a specific file

* `git status` -- show status

* `git commit` -- add comments 
	- `git commit -m 'Sample comments'
	- `git reset HEAD~1 -- Remove most recent commit

* `git remote add origin remote_repo_URL` -- add remote repo link/location

* `git push` -- Transfer all committed files to remote repo
	- `git push -u origin master`

* `git log` -- view commit history

* `git checkout .` -- revert back to the last committed version of github repo

* `git fetch` -- Fetch remote files to local directory 

* `git merge` --  Fetch remote files into CWD

* `git pull` -- fetch + merge
