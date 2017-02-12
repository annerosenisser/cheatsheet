# Cheat Sheet 
Most important bash commands for managing processes, Git, Python, R, SQL/SQLite and LaTeX for researchers and data scientists. This cheat sheet only focusses on bash commands run from the terminal.

****************************************************
****************************************************

## Table of Contents

 - [Managing processes](#managing-processes)    
 
 	- [First-aid procedure for killing a running process](#first-aid-procedure-for-killing-a-running-process)    
	- [Cronjobs and Crontab](#cronjobs-and-crontab)    
	- [Tmux sessions](#tmux-sessions)    
	- [Bash profiles](#bash-profiles)    
	
 - [Git](#git)     
 
 	- [Clone repository from GitHub to local machine](#clone-repository-from-github-to-local-machine)   
	- [Commit file from terminal](#commit-file-from-terminal)   
	- [Managing branches](#managing-branches)    
	- [global .gitignore file](#global-gitignore-file)   
	- [local .gitignore file](#local-gitignore-file)   
	- [Solve conflict using VIM editor](#solve-conflict-using-vim-editor)   
	- [Push commits from terminal with two-factor authentification](#push-commits-from-terminal-with-two-factor-authentification) 
	
 - [Python](#python)    
 
 	- [Virtual environments](#virtual-environments)    
	- [Check which python packages are installed](#check-which-python-packages-are-installed)    
	- [Start scrapy project](#start-scrapy-project)    
	
 - [R](#r)    
 	- [Open new window](#open-new-window)    
	- [Add R project to Github](#add-r-project-to-github)    
	- [Markdown and R](#markdown-and-r)    
	- [Options settings](#options-settings)    
	
 - [SQL and SQLite](#sql-and-sqlite)      
 	- [Repair corrupt database](#repair-corrupt-database)    
	- [Merge two SQLite databases](#merge-two-sqlite-databases)    
	- [Open new SQLiteBrowser window from terminal](#open-new-sqlitebrowser-window-from-terminal) 
	
 - [Text editing and LaTeX](#text-editing-and-latex)    
 	- [Calculate the number of words in a Latex file](#calculate-the-number-of-words-in-a-latex-file)    

****************************************************
****************************************************

## Managing processes

****************************************************

### First-aid procedure for killing a running process
* open new terminal window    
* type `ps + enter`    
* identify PID (processid) of the process    
* type `kill -9 <PID>`    

OR:    

* `control + C` (twice if needed)    


****************************************************

### Cronjobs and Crontab

#### Schedule crontab task
* If you want to run the cronjob on a server: enter the server
* enter `crontab -e` in the terminal
* enter `<minutes> <hours> <day of month> <month> <day of week>`
 * for example `6 0 * * 1-6 cd /home/annerose/Python/continuousscraper/ && python processcontrol.py`
 * this signifies that the process will start to run Monday through Saturday at 6 minutes past midnight.

For more information, see 

* [http://www.everydaylinuxuser.com/2014/10/an-everyday-linux-user-guide-to.html](http://www.everydaylinuxuser.com/2014/10/an-everyday-linux-user-guide-to.html) and    
* [http://stackoverflow.com/questions/12409101/scrapy-crawl-on-crontab-under-virtual-environment](http://stackoverflow.com/questions/12409101/scrapy-crawl-on-crontab-under-virtual-environment)    

#### Kill an existing cronjob
* enter `ps -e` in the terminal to see all existing processes.
* determine which processid your process has.
* enter `kill -9 <processid>`


****************************************************

### Tmux sessions
Tmux allows to keep processes running after ending an ssh session. For more detailed explanation, see [here](http://askubuntu.com/questions/8653/how-to-keep-processes-running-after-ending-ssh-session).

* ssh into the remote machine
* start tmux by typing `tmux` into the shell
* start the process you want inside the started tmux session
* leave/detach the tmux session by typing `Ctrl+B` and then `D`

You can now safely logoff from the remote machine, your process will keep running inside tmux. When you come back again and want to check the status of your process you can use `tmux attach` to attach to your tmux session.

If you want to have multiple session running side-by-side you should name each session using `Ctrl-B` and `$`. You can get a list of the currently running sessions using `tmux list-sessions`.

Some more useful tmux commands (see also this [video](https://www.youtube.com/watch?v=BHhA_ZKjyxo)):

| Command        | Significance          |
| ------------- |-------------| 
| `control + -b <command>`      | to tell the shell that it's for tmux and not just normal shell. | 
| `control + -b  p`    | previous window      | 
| `control + -b  n` | next window |
|`control + -b  c` | create window |
|`control + -b  w` | list windows |
|`control + -b %` |split window vertically into two parts |
|`control + -b` | split-horizontally : split window horizontally |
|`tmux - new s <sessionname>` | create a new tmux session |
|`control + -x`  | close (kill) tmux pane|
|`control + -b d` | detach from tmux session. (without stopping the process) |
| `tmux list-sessions` | List all tmux sessions|
|`tmux attach -t <sessionname>` | attach to a certain tmux session|
|`tmux attach` |attach all tmux sessions/ any tmux session |

****************************************************

### Bash profiles

#### Create bash profile

```bash
touch ~/.bash_profile; open ~/.bash_profile
```

`touch` creates the file, so no need to run this command when the file already exists. Alternative:

```bash
open ~/.bashrc
```

For editing the .bash_profile. opens in a text editor. See [here](http://stackoverflow.com/questions/30461201/how-do-i-edit-path-bash-profile-on-osx)

****************************************************

### Git

#### Clone repository from GitHub to local machine    
* create new repository on GitHub    
* go to the directory on your local machine where the cloned repository should be saved.    
* type `git clone https://github.com/your-name/repository-name.git`    
* the repository should now appear in the local folder on your machine.    

#### Commit file from terminal    
* go to the directory of your repository inside the terminal    
* type `git add .`  This recurses into sub-directories. Alternative: `git add` or `git commit -a`    
* `git commit -m “your commit message”`. Commit the changes.    
* `git push`. Push the changes.    

To see the status of your repository:  `git status`.

See [this](http://shaun.boyblack.co.za/blog/2009/03/14/getting-started-with-git-on-mac-os-x/) useful blog.

#### Managing branches
Branches are very important when you collaboratively work on Github. 

[This github page](https://github.com/Kunena/Kunena-Forum/wiki/Create-a-new-branch-with-git-and-manage-branches) contains useful information on how to create a new branch and how to manage branches on github. 

* go to the directory of your repository inside the terminal
* before creating a new branch, make sure all changes are pulled to your local repository
* Create new branch by typing `git checkout -b [name_of_your_new_branch]` 
* Push the new branch to github by typing `git push origin [name_of_your_new_branch]`
* Check out which branches exist for this repository: `git branch`. (If there is only the master branch, it will return `* master`.)
* Add a new remote for your branch: `git remote add [name_of_your_remote]`. A remote (URL) is Git's fancy way of saying "the place where your code is stored." (see [here](https://help.github.com/articles/about-remote-repositories/))
* Push changes from your commit into your branch (= into your remote): `git push [name_of_your_new_remote] [name_of_your_branch]`
* Update your branch from the original (master) branch: `git fetch [name_of_your_remote]`
* To merge changes between your branch and the original (master) branch, you should first switch to master branch in your terminal: `git checkout master`. Then simply type `git merge [name_of_your_branch]`.


#### global .gitignore file
See [here](http://stackoverflow.com/questions/7335420/global-git-ignore)

Create a global .gitignore file (file types to be excluded from every git project):  

```bash 
git config --global core.excludesfile ~/.gitignore_global
```

The file is found under Documents/Username (as a hidden file). Open it in a text editor to edit it and add files you don’t want to
sync with git/GitHub.

#### local .gitignore file
In the terminal, go to the working directory of the project you want to commit to github. 

```bash 
touch .gitignore
```  


The file is found locally in the working environment of the project. Open it in a text editor to edit it and add files.

#### Solve conflict using VIM editor
See this Stackoverflow post: [http://stackoverflow.com/questions/5599122/problems-with-entering-git-commit-message-with-vim](http://stackoverflow.com/questions/5599122/problems-with-entering-git-commit-message-with-vim)

If there is a conflict between your local version of the project and the version on Github, a window of the 
VIM editor will open after you've tried to commit your local changes. In this case, you should proceed as follows:   
* type `i` into the VIM editor, which opens the editing (**i**nsert") mode     
* type your merge message    
* press `Esc` to be sure to have left insert mode    
* then type `:wq` followed by `Enter`, which writes the current file and then closes it.    
* your merge should now have been accepted.

#### Push commits from terminal with two-factor authentification
See this helpful page on how to push commits from the terminal when using two-factor authentification on Github:   
[https://gist.github.com/wikimatze/9790374](https://gist.github.com/wikimatze/9790374)

**Important:** You need to use your personal access token, not your Github password to push commits from the terminal.

****************************************************
****************************************************

## Python

****************************************************

### Virtual environments

#### Change virtual environment: 

```bash
workon <name of virtual environment>
workon annerose2015-11  # python 2 environment
workon annerose_python3_2016-07 # python 3 environment
```

How to set up and manage virtual environments in Ubuntu:   [http://askubuntu.com/questions/244641/how-to-set-up-and-use-a-virtual-python-environment-in-ubuntu](http://askubuntu.com/questions/244641/how-to-set-up-and-use-a-virtual-python-environment-in-ubuntu)


#### Configure Pycharm to use a virtual environment

```bash 
touch ~/.pycharmrc; open ~/.pycharmrc
```    
See [here](see http://stackoverflow.com/questions/22288569/how-do-i-activate-a-virtualenv-inside-pycharms-terminal).

Then set the shell Preferences->Tools->Terminal->Shell path to  
`/bin/bash --rcfile ~/.pycharmrc`


****************************************************

### Check which python packages are installed

```bash
pip freeze
```

****************************************************

### Start scrapy project
Start [scrapy](http://scrapy.org) project for webscraping: enter the following command
in the terminal (in the directory where you want to start your project).

```bash
scrapy startproject name_of_project
```


****************************************************
****************************************************

## R

### Open new window
* Open new RStudio window from terminal (e.g. when one RStudio needs to run for an extended period of time):    
* enter `open -n -a "rstudio"` in terminal    
* How to add an RStudio project to Github: [https://www.r-bloggers.com/rstudio-and-github/](https://www.r-bloggers.com/rstudio-and-github/)    

### Add R project to Github
Add the following commands in shell after having created the project in Github:

```bash
git remote add origin https://github.com/your-name/repository-name.git    
git config remote.origin.url git@github.com:your-name/repository-name.git     
git pull origin master    
git push origin master    
```

### Markdown and R
Render/compile an R Markdown file from Terminal:  

```r
render("yourfile.Rmd")
```

[This](http://kbroman.org/knitr_knutshell/pages/Rmarkdown.html) resource on R Markdown is helpful.

An R Markdown cheatsheet is available from RStudio [here](https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf).

### Options settings

****************************************************
****************************************************

## SQL and SQLite

****************************************************

### Repair corrupt database
How to repair db database: see 
[stackoverflow](http://stackoverflow.com/questions/5274202/sqlite3-database-or-disk-is-full-the-database-disk-image-is-malformed)

```bash  
echo '.dump'|sqlite3 corrupt.db|sqlite3 corrupt_fixed.db    
cat <( sqlite3 corrupt.db .dump | grep "^ROLLBACK" -v ) <( echo "COMMIT;" ) | sqlite3 corrupt_fixed.db    
```

****************************************************

### Merge two SQLite databases

* [http://stackoverflow.com/questions/3689694/merge-sqlite-files-into-one-db-file-and-begin-commit-question ](http://stackoverflow.com/questions/3689694/merge-sqlite-files-into-one-db-file-and-begin-commit-question)    
* [http://stackoverflow.com/questions/80801/how-can-i-merge-many-sqlite-databases](http://stackoverflow.com/questions/80801/how-can-i-merge-many-sqlite-databases)

Leaving out duplicates:    

* [http://sqlite.1065341.n5.nabble.com/Merging-two-SQLites-leaving-out-duplicates-td46337.html](http://sqlite.1065341.n5.nabble.com/Merging-two-SQLites-leaving-out-duplicates-td46337.html)    

****************************************************

### Open new SQLiteBrowser window from terminal
[SQLiteBrowser](http://sqlitebrowser.org) is well suited for viewing and editing database files compatible with SQLite.

If you want to view several databases side by side, you have to open a new SQLiteBrowser window from terminal (it doesn't 
seem to be possible to open a new window from _within_ SQLiteBrowser). To this end, go to the directory where your
applications are stored (in Mac). Normally, this should be:

```bash
cd			# go to home directory
cd ../../..		# go three levels up
cd Applications		# go to Applications
```

Thereafter, type the command to open a new SQLiteBrowser window:

```bash
open -n sqlitebrowser.app
```

****************************************************
****************************************************

## Text editing and LaTeX

****************************************************

### Calculate the number of words in a Latex file
* change the working directory of your terminal to where the LaTeX TeX file is located.    
* enter `detex <document_name>.tex | wc -w -c -l` or just `detex <document_name>.tex | wc`    
* to calculate word count in pdf document: `pdftotext <document_name>.pdf - | wc -w`    
