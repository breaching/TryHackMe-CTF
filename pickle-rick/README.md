<div align="center">

# Pickle Rick Writeup



<img src="../img/pr.jpeg" alt="TryHackMe Logo" width="150">

---

| Machine Name | Room URL | Difficulty |
| :--: | :--: | :--: |
| <b>Daily Bugle</b> | <a href="https://tryhackme.com/room/picklerick">https://tryhackme.com/room/picklerick</a> | <img src="../img/green.png" alt="Logo 1" width="30">

<img src="https://tryhackme-badges.s3.amazonaws.com/670.png" alt="TryHackMe">

---
</div>

A Rick and Morty CTF. Help turn Rick back into a human!


# [Task 1] Pickle Rick

## #1.1 - What is the first ingredient that Rick needs?
 

```
nmap -sV -sC 10.10.71.25 
```
!["1.png"](files/1.png)

Based on the fact that port 80 (HTTP) is active, indicating the presence of a functioning web server, we can access the URL ```http://10.10.71.25 ```.

!["2.png"](files/2.png)

Let's do a quick check of the source code and search for hidden directories with dirb and nikto.

!["3.png"](files/3.png)
!["4.png"](files/4.png)
!["6.png"](files/6.png)
!["5.png"](files/5.png)

So, we found an username, maybe a password and an admin login page, so let's try.

!["7.png"](files/7.png)

It worked ! So now we got a command pannel connected to user `www-data`

!["8.png"](files/8.png)

Let's try to `ls -la` to check all the files in the directory.

```
total 40
drwxr-xr-x 3 root   root   4096 Feb 10  2019 .
drwxr-xr-x 3 root   root   4096 Feb 10  2019 ..
-rwxr-xr-x 1 ubuntu ubuntu   17 Feb 10  2019 Sup3rS3cretPickl3Ingred.txt
drwxrwxr-x 2 ubuntu ubuntu 4096 Feb 10  2019 assets
-rwxr-xr-x 1 ubuntu ubuntu   54 Feb 10  2019 clue.txt
-rwxr-xr-x 1 ubuntu ubuntu 1105 Feb 10  2019 denied.php
-rwxrwxrwx 1 ubuntu ubuntu 1062 Feb 10  2019 index.html
-rwxr-xr-x 1 ubuntu ubuntu 1438 Feb 10  2019 login.php
-rwxr-xr-x 1 ubuntu ubuntu 2044 Feb 10  2019 portal.php
-rwxr-xr-x 1 ubuntu ubuntu   17 Feb 10  2019 robots.txt
```

So we found two .txt files, let's check them.

!["9.png"](files/9.png)

And a clue.

!["10.png"](files/10.png)

Answer: `mr. meeseek hair`

## #1.2 - What is the second ingredient in Rick’s potion?

I attempted to get a reverse shell, but each time it shuts down, no matter how hard I try. So, don't go too deep into that rabbit hole. Also, our command panel filters certain queries like "cat," "head," "tail," etc. Luckily, we still have "find" and "less" for our needs. After using "ls -la /stuff/that/linux/have" to explore directories, I discovered this.

!["11.png"](files/11.png)

Answer: `1 jerry tear`

## #1.3 - What is the last and final ingredient?

I tried many commands to try to privesc and kept falling in a rabbit hole, in the end we just had to enter `sudo -l`

!["12.png"](files/12.png)

From now on we just need to open the 3rd flag by locating it.

!["13.png"](files/13.png)
!["13.png"](files/14.png)

Answer: `fleeb juice`
