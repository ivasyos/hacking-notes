# Wgel CTF thinking process

## Task 1 Wegl CTF

i have started the vpn and it was not working the ip adress is not working and i change the config file to asian then it worked

then i scan the netwrok using nmap

---

## 1 User flag

i have scaned the site with nmap and i found a ssh and http ports open

so on the siste just apache default page then i inspect and i found the message or comment

```
<!-- Jessie don't forget to udate the webiste -->
```

i have gobuster the site and i found cms called sitemap and i could't find anything

so i gobuster the /sitemap and i get .ssh in there there is id_rsa private key

so by my enum i found there is ssh and by my enumration i found out the user/developer called jessie and rsa private key

by that i am going to connect that's my analysis

so i was wrong when entering the username makeing the J capital letter other than that it work

thank to chatgpt to help me fix it

so in the doucument dir i found the user flag to be

```
057c67131c3d5e42dd5cd3075b198ff6
```

---

## Privilege Escalation (attempt)

for trying to previlage escalation i have found i can run wget as root with no password

and i go out to find the previlage escalation script in the gtfobins (i am new for that)

so i could't undestand it but with the help of ai i do but it's no good work

as u know chatgpt is dummy sometimes

so i try to talk to the leo brave broswer that i have a wget root

and it give me idea of to download the password in the shadow

and i do that using wget

and the password of the jessi or the user am in is in the hash

so cracking hash is hard for me (because i am new to this also)

so i check online tools which are not help full

so that i say i will conntriou tomorow or latter

but for today it's enough

---

## 2 Root flag

For day2 i tryied everything but no luck i will try latter

it's day 3 or 4 i don't know

what i do is i go to the and i cheated again but i was stuck

what i know is there is root_flag.txt file in the root dir

and i put up lister and with the sudo previlage i get using wget

i get the data from the root dir and send it to my machine

and when i look it it's this

```
b1b968b37519ad1daa6408188649263d
```

this is the answer

but i am not satisfyed with the work i do

i cheated i don't like

---

If you want next step, I won’t rewrite this — I’ll help you turn this exact thinking into **real skill (so next time you don’t get stuck or feel like you cheated)**.
