
###### Quick short cuts

```bash
# target discovery
nmap -sn -T5 <target> 

# disable ping and dns lookup for reverse dns lookup use -R
nmap -Pn -n <target>


```


###### Scripts


| Script           | Use                                                       |
| ---------------- | -------------------------------------------------------- |
| smb-os-discovery | system detai                                              |
| rdp-ntlm-info   rdp ntlm info, product version, DNS, NETBIOS,Target Name n,  |


Like most pentesting tools, nmap is run from the terminal. There are versions available for both Windows and Linux. For this room we will assume that you are using Linux; however, the switches should be identical. Nmap is installed by default in both Kali Linux and the [TryHackMe Attack Box.](https://tryhackme.com/my-machine)

Nmap can be accessed by typing `nmap` into the terminal command line, followed by some of the "switches" (command arguments which tell a program to do different things) we will be covering below.

All you'll need for this is the help menu for nmap (accessed with `nmap -h`) and/or the nmap man page (access with `man nmap`). For each answer, include all parts of the switch unless otherwise specified. This includes the hyphen at the start (`-`).

Answer the questions below

What is the first switch listed in the help menu for a 'Syn Scan' (more on this later!)?

-sS

Which switch would you use for a "UDP scan"?

-sU

If you wanted to detect which operating system the target is running on, which switch would you use?

-O

Nmap provides a switch to detect the version of the services running on the target. What is this switch?

-sV

The default output provided by nmap often does not provide enough information for a pentester. How would you increase the verbosity?

-v

Verbosity level one is good, but verbosity level two is better! How would you set the verbosity level to two?  
(**Note**: it's highly advisable to always use _at least_ this option)

-vv

We should always save the output of our scans -- this means that we only need to run the scan once (reducing network traffic and thus chance of detection), and gives us a reference to use when writing reports for clients.

What switch would you use to save the nmap results in three major formats?

-oA

What switch would you use to save the nmap results in a "normal" format?

-oN

A very useful output format: how would you save results in a "grepable" format?

-oG

Sometimes the results we're getting just aren't enough. If we don't care about how loud we are, we can enable "aggressive" mode. This is a shorthand switch that activates service detection, operating system detection, a traceroute and common script scanning.

How would you activate this setting?

-A

Nmap offers five levels of "timing" template. These are essentially used to increase the speed your scan runs at. Be careful though: higher speeds are noisier, and can incur errors!

How would you set the timing template to level 5?

-T5

We can also choose which port(s) to scan.

How would you tell nmap to only scan port 80?

-p80

How would you tell nmap to scan ports 1000-1500?

-p1000-1500

A very useful option that should not be ignored:

How would you tell nmap to scan _all_ ports?

-p-

How would you activate a script from the nmap scripting library (lots more on this later!)?

--script

How would you activate all of the scripts in the "vuln" category?
--script=vuln



NULL, FIN and Xmas TCP port scans are less commonly used than any of the others we've covered already, so we will not go into a huge amount of depth here. All three are interlinked and are used primarily as they tend to be even stealthier, relatively speaking, than a SYN "stealth" scan. Beginning with NULL scans:

- As the name suggests, NULL scans (`-sN`) are when the TCP request is sent with no flags set at all. As per the RFC, the target host should respond with a RST if the port is closed.  
    ![](https://assets.tryhackme.com/additional/imgur/ABCxAwf.png)  
      
      
      
      
    
- FIN scans (`-sF`) work in an almost identical fashion; however, instead of sending a completely empty packet, a request is sent with the FIN flag (usually used to gracefully close an active connection). Once again, Nmap expects a RST if the port is closed.  
    ![](https://assets.tryhackme.com/additional/imgur/gIzKbEk.png)  
      
      
      
      
    
- As with the other two scans in this class, Xmas scans (`-sX`) send a malformed TCP packet and expects a RST response for closed ports. It's referred to as an xmas scan as the flags that it sets (PSH, URG and FIN) give it the appearance of a blinking christmas tree when viewed as a packet capture in Wireshark.  
    ![](https://assets.tryhackme.com/additional/imgur/gKVkGug.png)  
    

  

  

The expected response for _open_ ports with these scans is also identical, and is very similar to that of a UDP scan. If the port is open then there is no response to the malformed packet. Unfortunately (as with open UDP ports), that is _also_ an expected behaviour if the port is protected by a firewall, so NULL, FIN and Xmas scans will only ever identify ports as being _open|filtered_, _closed_, or _filtered_. If a port is identified as filtered with one of these scans then it is usually because the target has responded with an ICMP unreachable packet.  

It's also worth noting that while RFC 793 mandates that network hosts respond to malformed packets with a RST TCP packet for closed ports, and don't respond at all for open ports; this is not always the case in practice. In particular Microsoft Windows (and a lot of Cisco network devices) are known to respond with a RST to any malformed TCP packet -- regardless of whether the port is actually open or not. This results in all ports showing up as being closed.  

That said, the goal here is, of course, firewall evasion. Many firewalls are configured to drop incoming TCP packets to blocked ports which have the SYN flag set (thus blocking new connection initiation requests). By sending requests which do not contain the SYN flag, we effectively bypass this kind of firewall. Whilst this is good in theory, most modern IDS solutions are savvy to these scan types, so don't rely on them to be 100% effective when dealing with modern systems.  

Answer the questions below

Which of the three shown scan types uses the URG flag?  

Xmas

Why are NULL, FIN and Xmas scans generally used?  

Firewall Evasion

Which common OS may respond to a NULL, FIN or Xmas scan with a RST for every port?

Microsoft windows

## Firewall evasion

We have already seen some techniques for bypassing firewalls (think stealth scans, along with NULL, FIN and Xmas scans); however, there is another very common firewall configuration which it's imperative we know how to bypass.

Your typical Windows host will, with its default firewall, block all ICMP packets. This presents a problem: not only do we often use _ping_ to manually establish the activity of a target, Nmap does the same thing by default. This means that Nmap will register a host with this firewall configuration as dead and not bother scanning it at all.

So, we need a way to get around this configuration. Fortunately Nmap provides an option for this: `-Pn`, which tells Nmap to not bother pinging the host before scanning it. This means that Nmap will always treat the target host(s) as being alive, effectively bypassing the ICMP block; however, it comes at the price of potentially taking a very long time to complete the scan (if the host really is dead then Nmap will still be checking and double checking every specified port).

It's worth noting that if you're already directly on the local network, Nmap can also use ARP requests to determine host activity.

---

There are a variety of other switches which Nmap considers useful for firewall evasion. We will not go through these in detail, however, they can be found [here](https://nmap.org/book/man-bypass-firewalls-ids.html).

The following switches are of particular note:

- `-f`:- Used to fragment the packets (i.e. split them into smaller pieces) making it less likely that the packets will be detected by a firewall or IDS.
- An alternative to `-f`, but providing more control over the size of the packets: `--mtu <number>`, accepts a maximum transmission unit size to use for the packets sent. This _must_ be a multiple of 8.
- `--scan-delay <time>ms`:- used to add a delay between packets sent. This is very useful if the network is unstable, but also for evading any time-based firewall/IDS triggers which may be in place.
- `--badsum`:- this is used to generate in invalid checksum for packets. Any real TCP/IP stack would drop this packet, however, firewalls may potentially respond automatically, without bothering to check the checksum of the packet. As such, this switch can be used to determine the presence of a firewall/IDS.  
    

Answer the questions below

Which simple (and frequently relied upon) protocol is often blocked, requiring the use of the `-Pn` switch?  

ICMP

**[Research]** Which Nmap switch allows you to append an arbitrary length of random data to the end of packets?

--data-length