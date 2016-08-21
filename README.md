# Bash Cheat Sheet 
Most important bash commands. 

The set-up of this cheat sheet is inspired by an existing [cheat sheet](https://github.com/tiimgreen/github-cheat-sheet) by [Tim Green](https://github.com/tiimgreen).


## Table of Contents
 - [Section](#github)
  - [Subsection](#ignore-whitespace)

## Cronjobs and Crontab
### Schedule crontab task
* If you want to run the cronjob on a server: enter the server
* enter `crontab -e` in the terminal
* enter `<minutes> <hours> <day of month> <month> <day of week>`
 * for example `6 0 * * 1-6 cd /home/annerose/Python/continuousscraper/ && python processcontrol.py new`
 * this signifies that the process will start to run Monday through Saturday at 6 minutes past midnight.

For more information, see 
* [http://www.everydaylinuxuser.com/2014/10/an-everyday-linux-user-guide-to.html](http://www.everydaylinuxuser.com/2014/10/an-everyday-linux-user-guide-to.html) and 
* [http://stackoverflow.com/questions/12409101/scrapy-crawl-on-crontab-under-virtual-environment](http://stackoverflow.com/questions/12409101/scrapy-crawl-on-crontab-under-virtual-environment)

### Kill an existing cronjob
* enter `ps -e` in the terminal to see all existing processes.
* termine which processid your process has.
* enter `kill -9 <processid>`


### Useful Articles
| Title | Link |
| ----- | ---- |
| GitHub Flow  | http://scottchacon.com/2011/08/31/github-flow.html |
