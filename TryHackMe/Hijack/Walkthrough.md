# Hijack
### Misconfigs conquered, identities claimed.

## I begin with an nmap scan for port discovery:
```
nmap -p- -T5 -Pn 10.10.146.229
```
## This machine has 9 open ports
INSERT SCREENSHOT HERE

## Next I run an nmap scan for those ports to discover version and operating system. 
```
nmap -sC -sV -O -p21,22,80,111,2049,46873,47540,50884,56455 10.10.146.229
```

## Browsing through the website, there are four main pages: Home, Administration, Login, and Sign up. 
## The Home page says: Welcome Guest This site is still under development!
