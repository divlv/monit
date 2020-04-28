# Dockerized version of Monit

Monit is a utility for managing and monitoring processes, programs, files, directories and filesystems on a Unix system and remote processes.

## Usage:

(All the sample files available in the GIT repository: https://github.com/divlv/monit)

### 1. Custom directory

Create directory for your custom configuration, e.g. `/opt/monit/customconfig`

### 2. setting.cfg

Add file `/opt/monit/customconfig/setting.cfg` with the following content:
```
set httpd port 2812 and
  use address 0.0.0.0
  allow admin:mymonit
```
Change at least login (admin) and password (mymonit).

### 3. myservices.rc

Add your configuration file here (with *.rc extension) e.g. `/opt/monit/customconfig/myservices.rc`
```
#
check host Wikipedia with address www.wikipedia.org
    if failed
        port 443
        protocol https
        # Add specific headers here, if needed
        #with http headers [Host: mmonit.com, Cache-Control: no-cache, Cookie: csrftoken=nj1bI3CnMCaiNv4beqo8ZaCfAQQvpgLH]
        and request / with content = "class"
        and timeout 10 seconds
    then alert
#
# Just check port alive:
check host My_SQL_Database with address db.example.com
    if failed
        port 1234
        and timeout 10 seconds
    then alert
#
```

### 4. Start service

Start docker image of *Monit* service like this:

```
docker run -d --rm --net=host -v /opt/monit/customconfig:/etc/monit/custom dimedrol/monit
```
* *--net=host* - use host network for enabling logins "from outside world"
* /opt/monit/customconfig - directory for your custom configs

Check your Docker host: http://mydocker.example.com:2812/
