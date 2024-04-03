roo<h1>Cyber Defense Project 1</h1>
<h2>Analyze a Remote Intrusion Attempt</h2>

<h3>Project Scenario</h3>
- Another analyst in our security operations center has seen evidence of a remote intrusion attempt on one of our client's infrastructures—a private network belonging to a long-time client AT-USA—and has captured a PCAP of the suspicious activity. I’d like you to analyze the PCAP and confirm or disconfirm malicious activity. I'd also like you to corroborate your initial conclusions by analyzing log data within the SIEM...not sure how well the activity was recorded in AT-USA's logging setup, but let's see if that adds any additional context to the event. <br>
- I'd like your report to be in SBAR (Situation/Background/Assessment/Recommendation) format—but since you're new to using the SBAR format, use the provided worksheet to document your investigation findings for now.

<h2>Project Roadmap</h2>
- Assess the situation by analyzing the PCAP <br>
- Search the SIEM to confirm your initial findings <br>
- Prepare SBAR Report.

<h2>Tools and Technologies Used</h2>
- Wireshark <br>
- Splunk <br>
- PCAP File <br>
- Amazon WorkSpaces as Virtual Machine 

<h2> 1. Assess the situation by analyzing the PCAP</h2> 
I Loaded the remote_intrusion.pcap into Wireshark to analyze the situation, <br>
and started articulating the initial hypothesis to be answered by the investigation. <br>

![PCAPloaded](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/4c56a31c-f0b8-4a33-a36a-bb37e75ec1be)


I documented all pieces of evidence to support the initial hypothesis. <br>
At this time I applied different filters in Wireshark to eliminate all the packets I deemed irrelevant. <br>


<img src="https://i.imgur.com/tP0zs1x.png" height="80%" width="80%" alt="Filtring for Evidence"/>


Now I eliminated all the packets that signify a failed login attempt since I was interested in a successful login attempt. <br>
Once I had removed all the handshake packets and failed login responses, I was down to a very small number of packets that made manual inspection of TCP streams a viable proposition. <br>
Finally, I identified all indicators of compromise from the Wireshark analysis including source and destination IP address and credentials the attacker used as well as a timeline of events that would serve as  pivots for Splunk analysis. <br>
<img src="https://i.imgur.com/x9b1rk4.png" height="80%" width="80%" alt=""/>

<h2> 2. Search the SIEM to confirm your initial findings</h2>
 I Configured Splunk for optimal search results as follows: <br>
- 1. Confirm mode is set to Verbose with no event sampling <br>
- 2. Set the timezone to GMT <br>
<p align="center">
Launch the utility: <br/>
<img src="https://i.imgur.com/NvyYGZo.png" height="80%" width="80%" alt=""/>
<img src="https://i.imgur.com/zzEnoaG.png" height="80%" width="80%" alt=""/>

 I log in with Splunk credentials. <br>
 I started Splunk search by specifying (1) a time interval, and (2) an SPL search command (the string in the search box) to retrieve specific logs.<br>
For example: when interested in firewall logs, I used index="firewall_asa" SPL and when interested in web traffic logs, I used index="web_apache" SPL, etc. <br>
<img src="https://i.imgur.com/5EfLpyw.png" height="80%" width="80%" alt=""/> <br>
I corroborated the evidence from wireshark with the evidence from the SIEM and concluded that there was a Brute-force attack on the AT-USA server on 12/06/2017 between 8:34:24 GMT - 18: 35: 33 GMT.<br> 
<img src="https://i.imgur.com/uAzBkDM.png" height="80%" width="80%" alt=""/> 

NOTE: The details of the analysis are Reported in the SBAR(Situation, Background, Assessment, and Recommendation) section of this page <b>

<h2> 3. SBAR Report</h2>
<img src="https://i.imgur.com/WMjiI0k.png" height="80%" width="80%" alt=""/> <br>
<img src="https://i.imgur.com/0wXcdRo.png" height="80%" width="80%" alt=""/> <br>

<img src="https://i.imgur.com/wnl5yyb.png" height="80%" width="80%" alt=""/> <br>
<img src="https://i.imgur.com/ioYpy9x.png" height="80%" width="80%" alt=""/> <br>
<img src="https://i.imgur.com/DXcv6B6.png" height="80%" width="80%" alt=""/> <br>
<img src="https://i.imgur.com/X9Nm1ea.png" height="80%" width="80%" alt=""/> <br>
<img src="https://i.imgur.com/PA4kUUv.png" height="80%" width="80%" alt=""/>

<h2>Note: The complete SBAR Report of this Project is Attached as a PDF Document in the Files Folder</h2>
