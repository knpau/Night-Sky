# Night-Sky

10s Interval Port Monitoring

[![Build Status](https://travis-ci.org/Ne00n/Night-Sky.svg?branch=Release)](https://travis-ci.org/Ne00n/Night-Sky)

Night-Sky is licensed under a Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License.
You should have received a copy of the license along with this
work. If not, see https://creativecommons.org/licenses/by-nc-sa/4.0/

- PHP 7.0+, using BackgroundProcess
- Run a Slot every Second, each Slot can run multiple Processes, 5 Servers are assigned to each Process
- Loadbalance the Monitoring requests over these Slots, 10 Slots per 10 Seconds, 1 Slot reserved for Offline Servers
- If a Port is not reachable, move it to the Dedicated Offline Slot, move it back afterwards (planned)
- Limit of 20 Users for the Start, 10 Checks for each User
- Email notifications via local Mail function (relayed to MXRoute)
- Block the current Thread if the previous one is still Running
- Database Backend: PHP, MariaDB
- Frontend: HTML (Bootstrap 3 / Font Awesome)

QuickSetup:

1. Create a User+DB, Import the content/sql/night-sky.sql
2. Rename content/configs/config.example.php to config.php and regex.example.php to regex.php
3. Configure content/configs/config.php:
- _Domain needs to be updated to the Domain you want to use, otherwise Cookies wont work.
- _mail_sender needs to be updated, to make contact work properly
- Finally you need to update the Database part, with the Details you created the Database with
- Make sure to use TLS on your Domain otherwise cookies will not apply on Plain.
- The rest can be edited on your needs,
4. Put cron/night.php and cron/remote.php into Crontab to run every 60 seconds, use a non privileged user for that.
5. Deploy some Remote Servers and add them to the table remote.<br />
- You can find the file for that in content/remote/<br />
- The Field IP can be also contain a URL like "check.domain.com", make sure the Domain is reachable over TLS, plain wont work.
