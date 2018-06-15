# CSF

CSF is [ConfigServer Security & Firewall](https://configserver.com/cp/csf.html). 
This is something that should keep away the Chinese bots

## Guides

### Installation

I forgot how to do that at the moment of writing... Pull request anyone?

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

