# Dockerized version of Monit

Monit is a utility for managing and monitoring processes, programs, files, directories and filesystems on a Unix system and remote processes.


Start *monit* service like this:

```
docker run -it --rm --net=host -v /opt/monit/customconfig:/etc/monit/custom mon6
```
* *--net=host* - use host network for enabling logins "from outside world"
* /opt/monit/customconfig - directory for your custom configs
