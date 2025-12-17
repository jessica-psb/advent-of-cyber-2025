# Day 1 [Linux CLI - Shells Bells]

## Objectives
- Investigate tbfc-web01 Linux server 
- Identify any suspicious activity related to McSkidy’s disappearance
- Gather findings to help restore Wareville’s defenses and prevent further compromise

## Main Task
Following the initial guidance, I proceeded by accessing the README.txt file to gather more information related to the challenge
```cat README.txt```

Inside the current directory, I identified a folder named Guides. Listing its contents, including hidden files, revealed a file called .guide.txt. Accessing this file led to the discovery of the first flag for the task. 
``` 
cd Guides
ls -la
cat .guide.txt
```
<img width="718" height="507" alt="image" src="https://github.com/user-attachments/assets/05fb19e2-85d0-40d8-b6d8-cfc5698e64d5" />

Check the /var/log/auth.log for failed login attempts that could indicate a brute-force attack.
```grep "Failed password" /var/log/auth.log```

This revealed multiple failed authentication attempts originating from a suspicious source. I checked whether any successful logins occurred following those attempts, which could confirm a compromised account.
```grep "socmas" /var/log/auth.log```
The results indicated that the same account was eventually accessed successfully, suggesting "socmas" account breach coming from eggbox-196.hopsec.thm.
<img width="952" height="400" alt="image" src="https://github.com/user-attachments/assets/faf1b8b2-87cc-46c1-9232-989b8395c8ea" />

I searched its home directory for files or directories associated with the attack, focusing on keywords linked to the brute-force activity and found 1 file.
```find /home/socmas -name "*egg*"```

Found second flag inside and then I examined the contents of the identified file to understand its purpose.
```cat /home/socmas/2025/eggstrike.sh```
<img width="587" height="212" alt="image" src="https://github.com/user-attachments/assets/6fb157e3-2d1b-4b31-8405-b7a869162377" />
The script steals the wishlist.txt content, deletes the original file, and replaces it with eastmas.txt as an act of sabotage.


I escalated privileges to the root account and reviewed the command history to identify any actions performed after the compromise.
```
sudo su 
history
```
<img width="711" height="292" alt="image" src="https://github.com/user-attachments/assets/45ce8cd2-d078-4285-90a4-80f087c9f856" />




