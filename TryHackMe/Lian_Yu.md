I first ping the system to verify it's up and running. 
```
ping 10.10.10.10
```
Next I run two nmap scans. The first one I use -p- to scan all ports instead of the top 1000, I use -T5 to speed up the scan and use -Pn to skip host discovery. 
```
nmap -p- -T5 -Pn 10.10.10.10
```
Then I rescan the live ports using -sV to find the version and -O to find the operating system. 
```
nmap -p21,22,80,111,46392 -sV -O 10.10.10.10
```

```
feroxbuster -u http://10.10.142.54 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
```

```
feroxbuster -u http://10.10.142.54 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -x ticket
```

```
exiftool aa.jpg
```

```
exiftool Leave_me_alone.png
```

```
exiftool Queen's_Gambit.png
```

```
hexedit Leave_me_alone.png
```

QUESTIONS
What is the Web Directory you found?
what is the file name you found?
what is the FTP Password?
what is the file name with SSH password?
user.txt
root.txt

SCREENSHOTS
