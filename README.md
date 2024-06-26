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

<h2>Experiencing the Beauty and the Simplicity of Filter pane in Wireshark</h2>


![Filter](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/ccb473ad-624b-4e28-a953-3004869abdac) 



Now I eliminated all the packets that signify a failed login attempt since I was interested in a successful login attempt. <br>
Once I had removed all the handshake packets and failed login responses, I was down to a very small number of packets that made manual inspection of TCP streams a viable proposition. <br>
Finally, I identified all indicators of compromise from the Wireshark analysis including source and destination IP address and credentials the attacker used as well as a timeline of events that would serve as  pivots for Splunk analysis. <br>

<h2>TCP Stream Evidence</h2>

![TCP Stream](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/4808d2a4-621e-488d-939d-6313637a610c)



<h2> 2. Search the SIEM to confirm your initial findings</h2>
 I Configured Splunk for optimal search results as follows: <br>
- 1. Confirm mode is set to Verbose with no event sampling <br>
- 2. Set the timezone to GMT <br>
<p align="center">
Launch the utility: <br/>


![SplunkConfig](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/6656523a-f266-4eda-86f2-95cafc00789c)





 <p>I log in with Splunk credentials. <br>
 I started Splunk search by specifying (1) a time interval, and (2) an SPL search command (the string in the search box) to retrieve specific logs.<br>
For example: when interested in firewall logs, I used index="firewall_asa" SPL and when interested in web traffic logs, I used index="web_apache" SPL, etc.</p> <br>


![Firewall](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/7cc14072-c83c-436a-921c-51d2274e075b)


<h2>Corroboration of Evidence</h2>

<p>I corroborated the evidence from wireshark with the evidence from the SIEM and concluded that there was a Brute-force attack on the AT-USA server on 12/06/2017 between 8:34:24 GMT - 18: 35: 33 GMT.</p> <br> 


![SIEM-Evidence](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/1fb7a982-badb-4b31-b3a1-400889b29564)




<h2>NOTE: The detail analysis are Reported in the SBAR(Situation, Background, Assessment, and Recommendation) section of this page</h1> <b>

<h2> 3. SBAR Report images</h2>

![situation](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/3ae5cc4c-7050-4d5c-8ad8-b148708c2b65)

![Background](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/e29b224a-d8a0-46a2-907d-5fe3c290b2ef)


![Capture](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/78f18387-5c70-4dfe-bfed-966a7a0a6ff4)


![Assessment](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/6daf75a1-12f3-4067-a816-92e93296465c)


![Assessment2](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/2962e2b2-8770-428c-82f7-e8d2cea737a3)


![Assessment3](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/45934c01-9dd7-408b-a98f-a69bd4a5c82e)


![Assessment4](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/8880a315-1a04-4021-9cd3-d3eb3644d4f7)


![Prevention](https://github.com/Alexoa4/Remote-intrusion/assets/105945708/bdf975e2-6d83-4edd-abd3-13040f52b1ae)

<h2>Note: The complete SBAR Report of this Project is Attached as a PDF Document in the Files Folder</h2>
