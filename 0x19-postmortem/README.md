<p align="center">
<img src="https://github.com/Helidah/alx-system_engineering-devops/blob/master/0x19-postmortem/500server.jpg" width=75% height=75%/>
</p>

## Service unavailability
### Incident report for [Site Outage] https://github.com/Helidah/alx-system_engineering-devops/blob/master/0x19-postmortem/500server.jpg)

#### Issue Summary
On February 22nd, 2022 from 12:02 AM to 5:47 AM EAT, the company's website was down for twenty minutes. 100% of users experienced a 500 internal server error caused by a misspelled filename in a configuration file.

#### Timeline
* 9:39 AM   Sitewide update deployed; outage begins
* 9:40 AM   Error logs checked by DevOps team
* 9:43 AM   Configuration updated to log extra errors
* 9:45 AM   Filename error caught in config file
* 9:47 AM   Execute Puppet manifest across all company servers
* 9:49 AM   100% restored and back online

#### Root Cause and Resolution
After a small sitewide update was deployed without the final testing, we experienced an outage to the site. When no errors were found in our 'error.log' files we modified our configuration file to allow for more error logging. With the help of 'strace,' it appeared a filename had been misspelt triggering errors when the site was requested. The server was attempting to locate the file as normal procedure but failed to find the file which was ending in ".phpp" when it should be looking for ".php". After changing this line in the '/var/www/html/wp-settings.php' file, tests were conducted and the site was functioning. A puppet manifest was written and executed across all company servers immediately after to restore service.

#### Corrective and Preventative Measures
Future methods to be implemented include:
* Modifying of configuration files for more error logging to quicken response times
* Testing will be done before deploying on all servers no matter how small an update

