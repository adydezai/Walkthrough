## Significance of Cron-Jobs in Pentesting

### What are Cron-Jobs and How can they help you get privileged access?

In a pentester's perspective Cron Jobs are one of may ways you can get SYSTEM to perform a task or a set of tasks. Jobs are scheduled periodically with freedom to perform tasks daily, weekly, monthly and so on. It is a convenient way for automatic updates, creating backups and is achieved by running scripts or executing commands periodically. 

**Below is how a crontab entries would look like!**
```markdown
**Example of job definition:**
.---------------- minute (0 - 59)
|  .------------- hour (0 - 23)
|  |  .---------- day of month (1 - 31)
|  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
|  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
|  |  |  |  |
*  *  *  *  * user-name  command to be executed
```
Cron Jobs can be found in **/var/spool/cron/crontabs** and should be accessible only by **root**.
Scheduled Cron Jobs can be listed using command and what this particular job does is obvious from the below script.
```markdown
# crontab -l
* * * * * cd /scripts; for f in *.py; do python "$f"; done
```
Let's dive in to get some shells!
Firstly lets get nmap to scan our target machine.
![nmapscan](https://user-images.githubusercontent.com/22067818/37248477-5fc43250-2527-11e8-9be8-1f4a62115d68.PNG)
Apparently there is a web server running, you can initiate a Nikto scan to enumerate more and meanwhile visit the site.
