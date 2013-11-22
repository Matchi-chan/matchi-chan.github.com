---
layout: post
author: Matchi-chan
title: 'Packet sniffing Valkyrie Crusade'
---

What happens when I packet-sniff a pretty good smartphone game that handles a lot of things server-side?

<!--break-->

Well, I decided to find out. The conditions for this are as follows:

-My Galaxy Note android phone connected to the family wifi, running the custom ROM ParanoidAndroid at the latest version.  
-Shark for Root/Shark Reader from the Play store.  
-A normal startup connection to VC (the "checking server data" screen that I know pulls in the data for new events and cards when it gives the green loading bar.)

To capture the data, I started Shark, clicked Start, long-pressed to get to the list of open applications and clicked VC, it did it's server checking, and as soon as I got back to my kingdom I long-pressed back to Shark and pressed Stop. This VC connection did not bring up the green bar as there isn't a new event or new cards yet. Also of note is that this time, it took longer than usual.

I then began to examine the packets with Shark Reader (there are well over a thousand, my god)

Just to say: I am not an expert in networking and security, this is the first time I've done a packet sniff.

-In the first 15 packets, there is an HTTP POST to http://api.m.renren.com for some reason, which is a Chinese social network. Must be related to the data recovery system that I have linked to my Twitter, seeing as the game is available in Chinese. [Screenshot]()

-A packet that says "connect nubee com" [Screenshot](http://i.imgur.com/SJeIRzu.png)

-Then, I found what must be the request body, as there's lots of telling things, such as JSON, com.nubee.valkyriecrusade and api_key=  [Screenshot](http://i.imgur.com/DkXjJBo.png)  
(which, if you know about kancolle's api_key, is something pretty exploitable and I should probably self-censor that screenshot so I don't lose my hours wasted to get to Lvl67) 

-After that, I find a HTTP request with JSON to an IP address, formatted like a HTTP POST. [Screenshot](http://i.imgur.com/zey2uIp.png) Connection: Keep-Alive definitely sounds like VC.

-valkyriecrusade.nubee.com in a packet.

-Then, there are a lot of huge packets which contain no plaintext for me to read but purely mojibake. Could be the actual server data coupled with encryption. The mojibake looks awfully like the Shift-JIS mojibake I'm used to seeing on Windows.

-Further down I find Google Analytics. Not sure if this is related to VC or it's just Android not respecting my freedums.

-GoDaddy and certificates for some reason. Get out of here.

-Lots and lots of 1440 size mojibake packets.

-Then, I find another good discovery: I can pretty much confirm that all connection is made using SSL, well at least they are using SSL. I've also seen hints in the packets above. [Screenshot](http://i.imgur.com/SJeIRzu.png)

-Some packets with valkyriecrusade.nubee.com in them coupled with mojibake. [Screenshot](http://i.imgur.com/kxP8MUy.png)

-M-SEARCH * HTTP/1.1 and Man: "ssdp:discover" formatted like a POST. [Screenshot](http://i.imgur.com/CSuzOta.png)

-All throughout the packets from the beginning I get a tiny one with just a string of "BJMB" my first thought is some kind of verification.

-Not so many huge mojibake packets now, but still a lot of it. I think most of the main communication has finished now and it's finishing up.

-api.twitter.com. This is either my Android client or the data recovery system for VC. Probably my client.

-Lots of VeriSign. No idea what this is.

-VeriSign mixed with Twitter. Yup, it's Twitter in some way.

-More GoDaddy and BJMB. Googling "BJMB in packets" returns a first result of a network worm. Oh dear...

-HTTP GET request to Google Analytics that that mentions Apex Launcher and my Android version. Google stop that.

That was fun. I can establish not much, but that connect.nubee.com is probably one of the servers and http://151.249.94:210/ and valkyriecrusade.nubee.com *could* be the game servers, it connects with SSL and uses HTTP/JSON. Going to those URLs in Chrome doesn't load anything, as I expected.




