I first ping the system to verify it's up and running. 
```
ping 10.10.195.108
```
![image](https://github.com/user-attachments/assets/064ab265-36c3-470c-a3c3-7bc8b6554c50)

Next I run two nmap scans. The first one I use -p- to scan all ports instead of the top 1000, I use -T5 to speed up the scan and use -Pn to skip host discovery. This system has five ports open: port 21 for FTP, port 22 for SSH, port 80 for a HTTP server, port 111 for rpcbind, and port 34788 is unknown.
```
nmap -p- -T5 -Pn 10.10.195.108
```
![image](https://github.com/user-attachments/assets/d504d4b1-9c62-4d19-8991-627690fb79ec)


Then I rescan the live ports using -sV to find the version and -O to find the operating system. 
```
nmap -p21,22,80,111,46392 -sV -O 10.10.195.108
```
![image](https://github.com/user-attachments/assets/e54e596c-a558-4edb-8179-e53857c2dfdd)

Next, I navigate to the website to find any clues. 
![image](https://github.com/user-attachments/assets/4771f5e1-c27f-49fa-8b56-ac9c92edaefd)

Looking at the source code, I notice the word "arrow" is bolded. Perhaps this could be a password?
<img width="959" alt="image" src="https://github.com/user-attachments/assets/606321cb-a1db-486b-adfe-27aabc5cd011">

To answer the first question, I run feroxbuster to scan the web server for a list of directories. We discover two notable directories: http://10.10.195.108/island/ & http://10.10.195.108/island/2100/.

```
feroxbuster -u http://10.10.195.108 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
```
![image](https://github.com/user-attachments/assets/97dc9541-d6ea-429f-a182-0e46b73ce6fd)

The first website gives me a message with the words Lian_Yu bolded and hints at a code word that is not there.

![image](https://github.com/user-attachments/assets/c72de9c7-45dc-4ea4-aa95-3895080b66bf)

After looking at the source code, I am presented with the code word which is v********.

<img width="516" alt="image" src="https://github.com/user-attachments/assets/caf56fa2-a9d9-4cf0-bb5b-7f6f982d5fc2">
![image](https://github.com/user-attachments/assets/0e1f833c-6776-4229-83be-fd15808ce620)
![image](https://github.com/user-attachments/assets/1da1365e-c0ee-4e95-b157-eba38dc38e29)


```
feroxbuster -u http://10.10.195.108 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -x ticket
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

