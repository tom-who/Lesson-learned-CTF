# Lesson Learned-CTF
A step by step walk through for Leson learned CTF on Tryhackme

# Link : https://tryhackme.com/room/lessonlearned

---

# Enumeration

Lets start like always with nmap, or if you prefer rustscan you are welcome to do that but anyways lets scan for any services running on any ports

Command `nmap <machine_ip> -sV -sC -p-` (*We use -sV for the service version and -sC to use scripts built into nmap for more data, and lastly we use -p- to scan for all 65,000 port instead of the first 1000*)

Anyways lets take a look at the results

![image](https://github.com/traveller404/Lesson-learned-CTF/assets/92340426/1c7ad258-a8db-46c7-b02e-abc5ba5f5d31) 

We see that port 22 and 80 are running
Considering the fact that port 22 is alot more secure than port 80 lets head over to the website by going to the following url **http://<machine_ip>**
It is a login page prompting a username and password

We dont have any current credentials to login with so we will have a look around first inspecting the source code also reveals nothing and using directory enumeration returns an /manual page which is an apache default page

Since we dont have anywhere else to look we have to start trying inject SQL code into the login page to try to return some useful information

WARNING: DO NOT USE 1' = '1

So when we are trying to inject SQL we have to be careful, as we soon learn that it can actually damage databases and sometimes might not even return anything. So now that is in mind, go over to https://book.hacktricks.xyz/pentesting-web/sql-injection

You can try out different symbols like "(" or "'" but that wont work, what I found worked for me is `1' UNION SELECT null-- -`  and putting that injection into the username query, and setting the password to anything you want

On this, you are greeted with:

![image](https://github.com/traveller404/Lesson-learned-CTF/assets/92340426/3cca8043-2ba2-4eab-a2ec-c09e46eabc53)

This expains what I mentioned earlier, being the fact 1' = '1 is dangerous because it can cause harm and not return much in reality
Anyways! 

Hope this helps
