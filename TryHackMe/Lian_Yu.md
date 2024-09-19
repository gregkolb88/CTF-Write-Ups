# Lian_Yu: A beginner level security challenge

## Enumeration

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

To answer the first question, I run feroxbuster to scan the web server for a list of directories. We discover two notable directories: http://10.10.195.108/island/ & http://10.10.195.108/island/2***/.

```
feroxbuster -u http://10.10.195.108 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
```

<img width="898" alt="image" src="https://github.com/user-attachments/assets/9c070390-8d6b-42b3-9850-0cd1e2a7bbc1">

The first subdirectory (http://10.10.195.108/island/) gives me a message with the words Lian_Yu bolded and hints at a code word that is not there.

![image](https://github.com/user-attachments/assets/c72de9c7-45dc-4ea4-aa95-3895080b66bf)

After looking at the source code, I am presented with the code word which is v********.

<img width="516" alt="image" src="https://github.com/user-attachments/assets/caf56fa2-a9d9-4cf0-bb5b-7f6f982d5fc2">

The second sub directory (http://10.10.195.108/island/2***/) gives me a message along with a youtube video that seems to have had the account deleted. 

![image](https://github.com/user-attachments/assets/0e1f833c-6776-4229-83be-fd15808ce620)

Checking the source code provides me with a message hinting that I should be looking for ".ticket". The period in that hint seems like it might be pointing to a possible file extension?

![image](https://github.com/user-attachments/assets/1da1365e-c0ee-4e95-b157-eba38dc38e29)

I run feroxbuster again on the web server, this time adding the -x option to search for file extensions. 

```
feroxbuster -u http://10.10.195.108 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -x ticket
```
<img width="895" alt="image" src="https://github.com/user-attachments/assets/cab66e53-8b33-4a7a-9d78-65cc8fc7fa85">

This was successful. Navigating to this subdirectory gives me what looks to be an encrypted password. 

![image](https://github.com/user-attachments/assets/3bd97948-f993-472b-b4ed-98c1423da49c)

After trying a few options using cyberchef (https://gchq.github.io/CyberChef/), it turned out to be encoded through Base58. Decoding it provided me with the FTP password. 

<img width="959" alt="image" src="https://github.com/user-attachments/assets/087ad0ac-aff8-4767-a995-588dc68b2397">

Next, I login into FTP with the credentials we found earlier. 

```
ftp 10.10.195.108
```

After logging into FTP and listing all the files, I am presented with four notable files (.other_user, Leave_me_alone.png, Queen's_Gambit.png, and aa.jpg). 

![image](https://github.com/user-attachments/assets/08a7ed69-e210-4a88-8960-f698b100e2b4)

I get them all for further evaluation. 

![image](https://github.com/user-attachments/assets/a5db7548-70d4-42b2-9568-c6595f80af4a)

First I read the .other_user file. This gives me a backstory on the character Slade Wilson. This is potenially another login name for FTP or SSH. 

```
cat .other_user
```

![image](https://github.com/user-attachments/assets/58f2956a-a747-47ed-874a-fb5edd27c48b)


Opening all of the pictures, two out of the three seem like ordinary pictures that are Arrow themed. However, the Leave_me_alone.png file is throwing an error saying it is not a png file. 

![image](https://github.com/user-attachments/assets/f42f62c4-604c-4a25-b95c-39f3a46d3f86)

![image](https://github.com/user-attachments/assets/9963cde7-45cd-4731-812a-e49a28fd0d29)

![image](https://github.com/user-attachments/assets/3e396376-7089-4faa-82a7-3149ff8fef9e)

After doing some research, it seems like I can adjust the hex code in an editor to potentially fix this. 

This is what the hex code was showing. I did indeed need to change the header. 

```
hexedit Leave_me_alone.png
```

![image](https://github.com/user-attachments/assets/195df849-7955-4c1d-9299-6ee7261bfd04)

Here is what the hex code should look like to reflect a .png file. 

![image](https://github.com/user-attachments/assets/a9bfb286-12c5-422e-bc9a-786bcea16629)

The picture now seems to indicat that it has something to do with the password. 

![image](https://github.com/user-attachments/assets/8bc30e27-9004-40fe-baef-d9983f3735fd)


![image](https://github.com/user-attachments/assets/5ffa5d0f-a92e-4914-a658-f3119de2f00e)



```
exiftool Queen's_Gambit.png
```
![image](https://github.com/user-attachments/assets/bc24714a-1ac2-4e3b-be72-c0006a51aae8)

```
hexedit Leave_me_alone.png
```





vigilante
!#th3h00d
