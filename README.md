# Bash Cheat Sheet 
Most important bash commands for researchers and data scientists. 

The set-up of this cheat sheet is inspired by an existing [cheat sheet](https://github.com/tiimgreen/github-cheat-sheet) by [Tim Green](https://github.com/tiimgreen).


## Table of Contents
 - [Managing processes](#managing-processes)
  - [First-aid procedure for killing a running process](#First-aid-procedure-for-killing-a-running-process)
  - [Cronjobs and Crontab](#cronjobs-and-crontab)
  - [Virtual environments](#virtual-environments)
  - [Tmux sessions](#tmux-sessions)
 - [Python](#python)
 - [R](#r)
 - [Text editing and LaTeX](Text-editing-and-LaTeX)
  -[Calculate the number of words in a Latex file](Calculate-the-number-of-words-in-a-Latex-file)

***
## Managing processes
### First-aid procedure for killing a running process
* open new terminal window
* type `ps + enter`
* identify PID (processid) of the process
* type `kill -9 <PID>`

OR:
* `control + C` (twice if needed)

### Cronjobs and Crontab
#### Schedule crontab task
* If you want to run the cronjob on a server: enter the server
* enter `crontab -e` in the terminal
* enter `<minutes> <hours> <day of month> <month> <day of week>`
 * for example `6 0 * * 1-6 cd /home/annerose/Python/continuousscraper/ && python processcontrol.py new`
 * this signifies that the process will start to run Monday through Saturday at 6 minutes past midnight.

For more information, see 
* [http://www.everydaylinuxuser.com/2014/10/an-everyday-linux-user-guide-to.html](http://www.everydaylinuxuser.com/2014/10/an-everyday-linux-user-guide-to.html) and 
* [http://stackoverflow.com/questions/12409101/scrapy-crawl-on-crontab-under-virtual-environment](http://stackoverflow.com/questions/12409101/scrapy-crawl-on-crontab-under-virtual-environment)

#### Kill an existing cronjob
* enter `ps -e` in the terminal to see all existing processes.
* termine which processid your process has.
* enter `kill -9 <processid>`

### Virtual environments
Change virtual environment: 

```bash
workon <name of virtual environment>
workon annerose2015-11  # python 2 environment
workon annerose_python3_2016-07 # python 3 environment
```

How to set up and manage virtual environments in Ubuntu: [http://askubuntu.com/questions/244641/how-to-set-up-and-use-a-virtual-python-environment-in-ubuntu](http://askubuntu.com/questions/244641/how-to-set-up-and-use-a-virtual-python-environment-in-ubuntu)


***
## R
* Open new RStudio window from terminal (e.g. when one RStudio needs to run for an extended period of time):
 * enter `open -n -a "rstudio"` in terminal
* How to add an RStudio project to Github: [https://www.r-bloggers.com/rstudio-and-github/](https://www.r-bloggers.com/rstudio-and-github/)

***
## Text editing and LaTeX
### Calculate the number of words in a Latex file
* change the working directory of your terminal to where the LaTeX TeX file is located.
* enter `detex <document_name>.tex | wc -w -c -l` or just `detex <document_name>.tex | wc`
* to calculate word count in pdf document: `pdftotext <document_name>.pdf - | wc -w`
