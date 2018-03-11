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
....
![nikto](https://user-images.githubusercontent.com/22067818/37248548-29b4779a-2529-11e8-87a1-9566794b1d42.PNG)

Nikto shows there is **/dev/** directory listing, and there is much to discover. Listing has two links :
![directorylisting](https://user-images.githubusercontent.com/22067818/37248580-bfee2da0-2529-11e8-88ca-4062b40ac841.PNG)

Have a look at **phpbash.php** file and will link the details: (https://github.com/arrexel/phpbash) read through!
What this does is gives you a code execution capability which can also be used to drop web shells on vulnerable websites. Good to Know!
Enumerating more into the system (LinuxPrivChecker.py or **cat /etc/passwd**), bring to you two user accounts of which **scriptmanager** (isnt that an unusual name? Hmm) interests more due to fact that it can access **/scripts** folder in **root** directory. 

Amazing! we can see a few scripts with **.py** extension. Thats not it, after a lot of drama to the point where frustration was so high that i left my listening port open for a long time and a downloaded reverse shell script in **/scripts** folder, at the same time trying to mess around with some other files. I got back to my listening shell and there you go, root dance with Cron-Jobs!

![rootdance](https://user-images.githubusercontent.com/22067818/37248686-8bd2b0e2-252c-11e8-8f72-dcebac5c1c12.PNG)

Cheers!
