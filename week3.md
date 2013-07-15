### 1. The /etc/passwd entries for the personal accounts of your group members.
---

    root:x:0:0:root:/root:/bin/bash
    .
    .
    .
    linus:x:1000:1000:Linus Torvalds,,,:/home/linus:/bin/bash
    nathan:x:1001:1001::/home/nathan:/bin/sh
    Mitch:x:1002:1002::/home/Mitch:/bin/sh
    
### 2. The list of processes started on your system at boot time, and a description of how each one was started.
---

     PID  PPID          COMMAND                     COMMENTS
       1     0          init [2]                    Started by inittab
       2     0          [kthreadd]                  Started by kthreadd
       3     2          [ksoftirqd/0]
       4     2          [kworker/0:0]
       5     2          [kworker/u:0]
       6     2          [migration/0]
       7     2          [watchdog/0]
       8     2          [migration/1]
       9     2          [kworker/1:0]
      10     2          [ksoftirqd/1]
      11     2          [kworker/0:1]
      12     2          [watchdog/1]

### 3. A list of the security advisories for your version of your OS, and the patches and updates you have installed.
---

We checked open ports before connecting to the network. We then installed sudo and openssh. After setting that up our ports are:

    Active Internet connections (servers and established)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State      
    tcp        0      0 *:ssh                   *:*                     LISTEN     
    tcp        0     48 128.223.203.11:ssh      wlan-nat-outside-:49519 ESTABLISHED
    tcp6       0      0 [::]:ssh                [::]:*                  LISTEN    

We will keep an eye on [debians security site](http://www.debian.org/security/).

After modifying /etc/apt/sources.list to include package mirrors from debian,
We ran:

    sudo apt-get update
    sudo apt-get upgrade

This installed various packages. A detailed list can be found in /var/log/apt/history.log which we've included.

    Start-Date: 2013-07-08  09:53:06
    Commandline: apt-get upgrade
    Upgrade: libkrb5-3:i386 (1.10.1+dfsg-5, 1.10.1+dfsg-5+deb7u1), 
    libkrb5support0:i386 (1.10.1+dfsg-5, 1.10.1+dfsg-5+deb7u1),
    libk5crypto3:i386 (1.10.1+dfsg-5, 1.10.1+dfsg-5+deb7u1), 
    libgssapi-krb5-2:i386 (1.10.1+dfsg-5, 1.10.1+dfsg-5+deb7u1)
    End-Date: 2013-07-08  09:53:13

__Kerberos runtime libraries__
_(a system for authenticating users and services on a network)_
* libkrb5-3
* libkrb5support0
* libk5crypto3
* libgssapi-krb5-2

### 4. Your plan for regularly checking for and applying updates from your OS distributor.
---
Added "0 2 * * 1 apt-get update -y > /dev/null &" to the crontab, so the system will update automatically, weekly.

__sudo apt-get update__ _(downloads the package lists from the repositories and "updates" them to get information on the newest versions of packages and their dependencies. It will do this for all repositories)_

__sudo apt-get upgrade__ _(will fetch new versions of packages existing on the machine if APT knows about these new versions by way of apt-get update)_

[source](http://askubuntu.com/questions/222348/what-does-sudo-apt-get-update-do)
    
    linus@olga:~$ sudo apt-get update
    Get:1 http://ftp.debian.org wheezy-updates Release.gpg [1,571 B]                            
    Get:2 http://ftp.debian.org wheezy-updates Release [116 kB]                                                  
    Hit http://http.debian.net wheezy Release.gpg                                                       
    Get:3 http://ftp.debian.org wheezy-updates/main Sources [733 B]                       
    Hit http://http.debian.net wheezy Release                                                  
    Get:4 http://security.debian.org wheezy/updates Release.gpg [836 B]                                       
    Get:5 http://security.debian.org wheezy/updates Release [102 kB]                 
    Get:6 http://ftp.debian.org wheezy-updates/main i386 Packages [630 B]        
    Hit http://http.debian.net wheezy/main Sources                                                       
    Get:7 http://security.debian.org wheezy/updates/main Sources [42.3 kB]        
    Get:8 http://ftp.debian.org wheezy-updates/main Translation-en [520 B]        
    Get:9 http://security.debian.org wheezy/updates/main i386 Packages [81.1 kB]                 
    Hit http://http.debian.net wheezy/main i386 Packages                           
    Get:10 http://security.debian.org wheezy/updates/main Translation-en [45.9 kB] 
    Hit http://http.debian.net wheezy/contrib i386 Packages                                                  
    Hit http://http.debian.net wheezy/non-free i386 Packages
    Hit http://http.debian.net wheezy/contrib Translation-en
    Hit http://http.debian.net wheezy/main Translation-en
    Hit http://http.debian.net wheezy/non-free Translation-en
    Fetched 392 kB in 3s (117 kB/s)
    Reading package lists... Done
    linus@olga:~$ sudo apt-get upgrade
    [sudo] password for linus: 
    Reading package lists... Done
    Building dependency tree       
    Reading state information... Done
    0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.


