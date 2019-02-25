# CSF

CSF is [ConfigServer Security & Firewall](https://configserver.com/cp/csf.html). 
This is something that should keep away the Chinese bots

## Guides

### Installation

[Original Source](https://download.configserver.com/csf/install.txt)

    cd /usr/src
    wget https://download.configserver.com/csf.tgz
    tar -xzf csf.tgz
    cd csf
    sh install.sh

Test if everything works on the server

    perl /usr/local/csf/bin/csftest.pl

If you previously had any other iptables firewall, you need to remove
it. You can use this script. Run just in case

    sh /usr/local/csf/bin/remove_apf_bfd.sh

Now don't forget to whitelist your IPs

Disable testing in `/etc/csf/csf.conf` and most importantly
remove `22` port from config. This will stop SSH connections
from IPs not defined in csf.allow file.

    cd /etc/csf
    nano csf.conf

Start csf firewall

    csf -s

Now restart server or lfd service

    service lfd restart
    
**Don't forget to disable testing mode after whitelisting the correct IPs!**

### Whitelisting an IP

1. Connect to SSH
2. Switch to root
3. Go to `/etc/csf`
4. Edit `csf.allow` file and add desired IP address
5. Restart csf

Here's how that would look in the terminal

```
sudo su
cd /etc/csf
nano csf.allow
csf -r
```

