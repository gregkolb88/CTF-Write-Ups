# Archangel

## Description

### Boot2root, Web exploitation, Privilege escalation, LFI

## Recon
I begin by running two nmap scans. This first is run on all ports, ensuring I don't miss any obscure ports, using -T5 to expedite it and skipping host discovery. The second is to gather the version and OS for the target. 
```
nmap -T5 -Pn -p- 10.10.102.184
```
![image](https://github.com/user-attachments/assets/77e022e2-bcc5-47e3-8e40-745a2c4141ff)

```
nmap -sV -O -p22,80 10.10.102.184
```
