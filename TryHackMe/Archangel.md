# Archangel

## Description

### Boot2root, Web exploitation, Privilege escalation, LFI

## Recon
I begin by running two nmap scans. This first is run on all ports, ensuring I don't miss any obscure ports, using -T5 to expedite it and skipping host discovery. The second is to gather the version and OS for the target. 
```
nmap -T5 -Pn -p- 10.10.102.184
```
```
nmap -sV -O -p22,80 10.10.102.184
```
![image](https://github.com/user-attachments/assets/d25c18f6-96ce-45e7-8ce7-dcac36cd9ce4)


Find a different hostname
The answer to this is right up at the top of the main webpage. 
![image](https://github.com/user-attachments/assets/bd68d775-75c0-4b03-a972-c3240b73275d)

I added the newly discovered hostname to the hosts file then navigated to that webpage. The flag is found with a website showing the page is under development. 
Find flag 1
![image](https://github.com/user-attachments/assets/04933dea-d5af-48ea-ada8-6f7fdf03ad92)

Look for a page under development
Find flag 2
Get a shell and find the user flag
Get User 2 flag 
Root the machine and find the root flag
