# Lab: Network Sniffing
## About
- Author: Logan Cessac
- Course: IS 3513-01T
- Professor: Eric Wooldridge
- Date Created: July 31, 2026
- Purpose: To find patterns with my personal network using Wireshark

NOTE: I've hidden the following information to prevent releasing answers to the lab questions or revealing personal device information:
- Filenames and paths
- IP and MAC addresses


## Method and Experience
I was grateful because I have used Wireshark briefly before. It was one of the tools used in a lab for one of my classes. This helped familiarize me with the application. I began by opening Wireshark and started a capture. Then I made sure to select my Wi-Fi adapter to analyze traffic on just that interface. It was also the only adaptor with a continuous flow of traffic. I let it run for 11 seconds, which I confirmed by checking the capture file properties (See Figure 1). I captured 7199 packets in 11 seconds. I decided to save the capture to my files to analyze it in the future. This allowed me to make observations even if I closed the application. This proved useful because I had to switch between multiple networks when my Wi-Fi went out. I put that into a folder with my lab documents. I used the filter bar at the top to quickly filter through each of the protocols. This worked for most of the protocols. However, HTTP, FTP and ICMP protocols required some extra steps. I found that ARP traffic accounted for about 0.3% of my traffic (See Figure 2). TCP accounted for 18.5% of my traffic (See Figure 3). UDP accounted for 81.2% of my traffic (See Figure 4). HTTPS accounted for 5.5% of my traffic (See Figure 6). DNS accounted for 0.7% of my traffic (See Figure 9). There is slight overlap, which I believe because a portion of packets were counted twice in two different filters. 

Capturing HTTP traffic seemed difficult when it didn’t show up in the filter, but I then realized that all I have to do is access a website that uses HTTP instead of HTTPS. I found a website that was designed for this, which was reassuring, because I’ve heard about security concerns with HTTP traffic. I accessed the following website during the capture, which produced the desired results (See Figure 5): “http://uniquecoolslowplan.neverssl.com/online/.” Once I saw traffic under the HTTP filter, I ended the capture and closed out the website.

For the FTP filter, I went to the command prompt and typed in “ftp ftp.gnu.org” without entering the command. Then I started a capture in Wireshark with the FTP filter on. I returned to command prompt and pressed “enter.” I put in “anonymous” as the username. It gave me access, so I entered “dir” and then “quit” to test a command and then exit the ftp connection. I stopped the capture and viewed the results (See Figure 7). Finally, I saved the results to a file for future reference. This was a difficult process to work through, because of outdated resources. The video link in Step 7: Part (f): used a website as an example that didn’t work for me. However, after I found a better website to establish an FTP connection with, the rest of the process was much easier. 

To find ICMP packets, I went through a similar process to the FTP capture. I entered “ping 8.8.8.8” while capturing with the ICMP filter on to be able to pick up ICMP packets. After the command cycled through its four pings, I ended the capture and analyzed the results (See Figure 8). I then saved the results to a file for future reference. Pings make the most sense for testing ICMP traffic, because it is a simple and easy option, but can show whether ICMP traffic is being captured.

I wanted to set my 1-hour capture to exactly one hour, so I opened the “Options” menu under the “Capture” tab in the top ribbon. Here I set the capture to end automatically after exactly one hour. I also added a precaution by setting a maximum size for the capture so it couldn’t possibly crash my computer. I set the maximum storage size to 1GB. Once I had these settings entered, and I had restarted my network connection, I started the capture. I closed out each software that was open except for Word, which I was using to write my lab. I stopped writing for about 15 minutes and watched the capture. About this time, it was at about 9000 packets captured. I started writing in Word. After a few seconds, I checked my capture, and it had jumped to well over 50,000 packets. I immediately closed the software to conserve storage. The rest of the capture produced only about 10,000 more packets with a total of 61,845 packets. The most common protocol was TCP with about 91.9% of the capture consisting of this protocol. This is a very different trend from the first capture where TCP traffic only accounted for 18.5%. My guess for this is that certain applications I was running used other protocols, but when idling, TCP is a more common protocol. I also noticed that each time my computer would sleep, and I would wake it up, I would see a spike in network activity. I checked the I/O graphs to see if my suspicions were correct about network spikes. I found that I was correct. When I used Word, there was a spike of about 41,000 packets. I woke up my computer twice during the hour. Each occurrence displayed a spike of about 2,000-4,000 packets. For the rest of the time there was little network activity. I verified that the capture ran for about an hour (See Figure 10).

For the overnight capture, I had to get creative. I did not want the Wi-Fi connection to pause while my computer slept, so I entered settings and found the battery and screensaver settings. I changed the automatic sleep settings to not turn my screen off for several hours, which would give Wireshark enough time to finish the capture. I also worried about storage, so I put in a maximum capture size of 1GB. The last capture, which spanned about one hour, occupied about 60MB. The overnight capture should only take up about 200-300MB. I set a time limit to shut the capture down after five hours. I also shut down every other application to promote a steady amount of traffic. When I woke up, I found a few interesting patterns. Wireshark captured a total of 60,177 packets, which surprised me, because the 1-hour capture totaled about the same. I got up in time to stop the capture before it naturally ran through the full five hours. It ran for about 4 hours and 49 minutes (See Figure 11). I was also interested to see that, when I saved the capture to a file, it occupied about 36MB, which is a little more than half of the 1-hour capture. When I looked at the I/O graphs, which showed me that there was only one spike of about 3500 packets, and that the rest of the capture was relatively consistent. TCP was still the most common protocol with 74.2% of the capture consisting of this protocol.

Making a diagram for this lab was relatively easy. I already knew the network configuration for my house, which happens to be very similar to network structure in the example. I went to Google Docs to use the “Insert Drawing” option, which allows me to make shapes and lines to make a diagram. I inserted a few shapes, labeled them appropriately, and connected them with lines to create a picture that accurately portrays my home’s network. Then I copied it over to my main lab and added a border, so that it’s easier to see (See Figure 12). I use a wireless access point, which has been nice, because that allows me to move my workstation without rewiring any rooms. It also allows others to join my network if need be. 

My final activity was to compare the network traffic with my observed IP and MAC address for this device. I opened the 1-hour capture and filtered the results with the ARP filter. I analyzed the most common IP and MAC addresses in the capture to find a match (See Figure 13). I also opened Command Prompt, and, Using the common “ipconfig /all” command, I navigated to network adaptor that I used during the capture, which was labelled “Wireless LAN Adaptor Wi-Fi” (See Figure 14). The IP address was "IP Address" and the MAC address was "MAC Address." Once I was finished with my activities, I closed out Command Prompt and Wireshark.

## Associated Research
Wireshark is packet sniffing tool that was developed in 2006. It was derived from a previous software named Ethereal, which was created in 1998. It was then maintained by Gerald Combs and Jeffrey Foster and released for use in 2002. It was released for use What set Ethereal apart in its early years was that it “used the GTK+ widget to implement its graphical user interface that also used multiple widget toolkits.” (Hashim et al. 2025) It also included the same hexadecimal view of data that Wireshark currently employs. The tools and layout of Ethereal were the basis that led to the creation of Wireshark. Ethereal started declining in popularity, but that was when Wireshark started to become more widespread. Soon, it would go on to become “the most prevalent network analysis tool worldwide.” (Kaya, Ozdem, and Das 2025) Wireshark has been in use for about 20 years, which speaks to the reliable nature of the application. It has been relatively time-tested. Its real-time nature

Wireshark is a tool that can be used to sniff network traffic for analysis. The data that can be generated with Wireshark is invaluable, because it can lead to critical conclusions about a network’s architecture. It can analyze the amount of network traffic passing through a device, the type of traffic passing through, and the status of connections when they were created. It can not only be used for simple household use on personal computers, but it can be used on larger networks such as backbone networks with much larger amounts of data. I was able to draw simple conclusions from a capture, but larger corporations may need to use this tool for capturing several megabytes of data, several gigabytes of data, or more. It is a great tool with many flexible options, such as provide “functionalities to read data traffic in various formats, filter out irrelevant data traffic, analyze, and display traffic and metadata, and decompose traffic to check all the connections and data exchanges.” (Hashim et al. 2025) Metadata, or data about the data, is helpful in coming to conclusions about potential anomalies or even just promoting healthy network architecture practices. It is easy to install and set up on a typical device. It is flexible between different operating systems, and it is “packed with various advanced features including sharing the captured traffic with others.” (Hashim et al. 2025) With large amounts of data, some programs can’t handle a flood of data. Wireshark’s design allows it to not only capture all traffic and generate reports, but open pcap files of large sizes in less than a second. It is also good for troubleshooting network problems. Because it can analyze all data that passes through a device, it can help to “trace down those problems which causes poor performance, intermittent connectivity using appropriate driver support.” (Jain and Anubha 2021) The reason it can analyze large amounts of data is because it supports a wide variety of protocols. While some programs only look for a certain protocol, Wireshark can handle several, informing the user the amount and type of data flowing through their machine. It is maneuverable because “it supports a large number of networking protocols, giving it a flexible tool for examining various kinds of network data.” (Sivagaminathan et al. 2023)  Another benefit to Wireshark is its compatibility with other applications, such as Snort. Compatibility with other applications is critical for saving time in an organization that uses several platforms and services. It opens the door to automation, but even if not, it saves the user keystrokes and manual input. Many times, the data from Wireshark is used as input for another program, which can process other aspects of the log file. Python can be used for more powerful data analysis, such as “python module integration.” (Kaya et al. 2025) Certain data from other applications can be opened in Wireshark and analyzed. It has many built-in features that other programs don’t offer. Log files can be “exported to Wireshark to examine the captured network packet.” (Jain and Anubha 2021) exports and saves from Wireshark include pcap and pcapng file types, but there are many different export types. Some like to convert to a csv file to perform comprehensive data analysis. This is good for static data. The pcap format is a good option for dynamic data, but “Static integration, on the other hand, utilized the CSV format.” (Kaya et al. 2025) Another advantage of using Wireshark is that it’s very user friendly. When I used it, I appreciated the fact that there are graphical interfaces for handling data and creating analysis charts. Entries can be color-coded, which makes anomalies much easier to spot. I’m not the only one. One of the most widely attractive aspects to Wireshark is its GUI, which makes it “simple to explore and analyses network traffic. Additionally, it offers a number of visualization tools, including packet decoding, protocol dissectors, and graphs, to make it simpler to comprehend the data being gathered.” (Sivagaminathan et al. 2023) 

There are, however, some limits to Wireshark which are important to consider. One of them is that it cannot act based on what it detects. It is able to analyze traffic passing through, but it doesn’t make decisions or raise flags to certain traffic automatically. While it can analyze certain information dynamically with decryption standards, it is still “not sufficient to create effective live attack detection systems.” (Kaya et al. 2025) SIEM tools are very useful for generating flags and using machine learning to detect complex and subtle anomalies. However, while Wireshark may be used to sniff out packets, state overall statistics, and conduct simple analyses, it is not designed to perform the next-level detection that good SIEM tools can provide. In fact, Wireshark can be seen or used as a steppingstone to SIEM tools, because every SIEM starts with logs, which Wireshark can produce. Though it may process information and draw reasonably valuable conclusions, it is widely used as a beginning tool that provides information to other programs, which can handle much more complex calculations. 

Overall, though, Wireshark is a uniquely powerful tool that is recognized world-wide for its exceptional performance. Other tools are helpful, but Wireshark is considered the standard in packet sniffing and basic network analysis. Its best strengths are ease-of-use and compatibility. It is known for its ability to integrate with many areas of a company. It can be helpful for many fields and professions, but for a cyber threat analyst, it is pivotal in understanding the target network. It is not the first packet sniffing tool, and it is not, by any means, the only useful tool in network analysis and architecture. Cisco Packet Tracer, for example, can “build a network in a simulated environment,” which could be very useful in ways Wireshark cannot fulfill. (Sivagaminathan et al. 2023) However, it is one that I will need to know as a potential analyst one day. Some useful skills for me to learn with Wireshark are integration techniques, statistics analysis, and pattern recognition. Integration techniques will help me find ways to save me and the company I work for time and money. Statistics analysis will give me the ability to see what a network does. That answers the question of what is happening in a network. When are its critical moments? Why does it succeed or fail? Where is the problem? Pattern recognition could help me see a problem before it ever arises. My goal in analysis is to prevent disasters from ever even happening. If I can learn to find the patterns that repeat before most disasters, I can do a better job in preventing serious damage to my company. 

## Appendix
<details>
  <summary> Click to view Figures</summary>

  - Figure 1: Wireshark Capture File Properties
<img width="624" height="362" alt="Picture1" src="https://github.com/user-attachments/assets/c78a8be8-2d03-4b45-8668-587b9cd14e79" />

- Figure 2: ARP filter applied
<img width="624" height="116" alt="Picture2" src="https://github.com/user-attachments/assets/9db9449b-f101-495d-8342-585adc883d5c" />

- Figure 3: TCP filter applied
<img width="627" height="151" alt="Picture3" src="https://github.com/user-attachments/assets/9ab56720-a679-4bf5-83a1-d868748ca5ba" />

- Figure 4: UDP filter applied
<img width="624" height="137" alt="Picture4" src="https://github.com/user-attachments/assets/76ae536d-ae98-482e-a899-c3dc7bbc96b7" />

- Figure 5: HTTP filter applied
<img width="629" height="120" alt="Picture5" src="https://github.com/user-attachments/assets/4b1c6646-aedd-4799-bf49-ed10798d9a57" />

- Figure 6: HTTPS (TLSv1.2) filter applied
<img width="624" height="128" alt="Picture6" src="https://github.com/user-attachments/assets/6c2839ea-f2d3-46a2-8c8e-2fb57e3ad76f" />

- Figure 7: Successful FTP Capture
<img width="624" height="147" alt="Picture7" src="https://github.com/user-attachments/assets/a941a331-1852-44b2-b1f4-b097f29db733" />

- Figure 8: ICMP filter applied with ping test
<img width="624" height="126" alt="Picture8" src="https://github.com/user-attachments/assets/7333a776-978d-4466-ac11-6e7c056c62a2" />

- Figure 9: DNS filter applied
<img width="624" height="141" alt="Picture9" src="https://github.com/user-attachments/assets/abbc11f1-c834-4e63-a696-f9562825cde3" />

- Figure 10: One-Hour Scan Network Statistics
<img width="538" height="545" alt="Picture10" src="https://github.com/user-attachments/assets/3f2693c7-3b82-49d0-a6c1-785560e995e8" />

- Figure 11: Overnight Scan Network Statistics
<img width="624" height="460" alt="Picture11" src="https://github.com/user-attachments/assets/275dc886-e95c-45ae-85eb-d12911137db6" />

- Figure 12: Home Network Diagram
<img width="377" height="581" alt="Picture12" src="https://github.com/user-attachments/assets/d2839805-1c19-428c-91f4-51f7d7bc5bb5" />

- Figure 13: ARP with MAC and IP Address
<img width="624" height="120" alt="Picture13" src="https://github.com/user-attachments/assets/5b47ecbd-2ee7-4a00-b288-2b41f228ca86" />

- Figure 14: MAC address and IP address in Command Prompt
<img width="624" height="224" alt="Picture14" src="https://github.com/user-attachments/assets/8551fd25-2a24-4b95-a988-a7697d0b2a45" />

  
</details>

## Bibliography
<details>
  <summary> Click to view sources</summary>
  
- Hashim, S. R., Abdulhamed, M. K., & Abdalhameed, N. K. (2025). Detecting network activity using the Wireshark utility. AIP Conference Proceedings, 3350(1), 080035. doi:10.1063/5.0298413
- Jain, G., & Anubha. (2021). Application of SNORT and Wireshark in network traffic analysis. IOP Conference Series: Materials Science and Engineering, 1119(1), 012007. doi:10.1088/1757-899X/1119/1/012007
- Kaya, M. O., Ozdem, M., & Das, R. (2025). A novel approach for graph-based real-time anomaly detection from dynamic network data listened by Wireshark. EAI Endorsed Transactions on Industrial Networks and Intelligent Systems, 12(2), 16. doi:10.4108/eetinis.v12i2.7616
- Sivagaminathan, V., Sharma, M., & Henge, S. K. (2023). Intrusion detection systems for wireless sensor networks using computational intelligence techniques. Cybersecurity, 6(1). doi:10.1186/s42400-023-00161-0
  
</details>


