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
<img src="https://i.imgur.com/YfV85Ux.png" height="80%" width="80%" alt="Loading PCAP"/>
and started by articulating the initial hypothesis to be answered by the investigation. <br>
I documented all pieces of evidence to support the initial hypothesis. <br>
At this time I applied different filters in Wireshark to eliminate all the packets I deemed irrelevant. <br>
Now I eliminated all the packets that signify a failed login attempt since I was interested in a successful login attempt. <br>
Once I had removed all the handshake packets and failed login responses, I was down to a very small number of packets that made manual inspection of TCP streams a viable proposition. <br>
Finally, I identified all indicators of compromise from the Wireshark analysis which would serve as  pivots for Splunk analysis.

<h2> 2. Search the SIEM to confirm your initial findings</h2>
 I Configured Splunk for optimal search results as follows: <br>
- 1. Confirm mode is set to Verbose with no event sampling <br>
- 2. Set the timezone to GMT <br>

 I log in with Splunk credentials. <br>
 I started Splunk search by specifying (1) a time interval, and (2) an SPL search command (the string in the search box) to retrieve specific logs.<br>
For example: when interested in firewall logs, I specify index="firewall_asa" and when interested in web traffic logs, I used index="web_apache" etc. 


<h2> 3. SBAR Report</h2>
<p></p>From: Greg Clifford
Sent: Aug 9, 2023
Status: Feedback pending
 

 

Your submission
IMPORTANT: For ANY question you are not able to determine the answer to, you must do the following: (1) in your answer to that question, explicitly state that there is insufficient information available to determine the answer, & (2) include an appropriate RECOMMENDATION requesting access to whatever additional evidence sources would allow you to actually answer that question.

 

SITUATION
The SITUATION section provides a fairly brief overview of the situation or incident that triggered the investigation you are about to undertake.

SITUATION should contain NONE of your conclusions or findings determined after actually beginning your investigation. All investigation findings belong in the ASSESSMENT section.

S1 Write a 1-2 sentence summary of the instigating incident or "situation" that kicked off this investigation in the first place.

This is Alexander from the IT Security Team here, reporting a potential security breach impacting one of our client's infrastructures.

An Analyst from our Security operations center had evidence of a remote intrusion attempt on 12/06/2017 involving AT-USA infrastructure and captured a PCAP of the suspicious activity.

S2 If this investigation concerns a particular client, name it here. (Upon whose behalf are you conducting this investigation?)

 

This suspicious activity is impacting the network infrastructure belonging to a long-time client, AT-USA.

S3 Reiterate any relevant hypotheses or observations included in whatever information you were provided at the onset about the instigating incident.

I believe by analyzing the captured PCAP I would be able to confirm or disconfirm if the activity was malicious.

I believe by analyzing the captured PCAP I would be able to confirm or disconfirm if the activity was remotely generated or not.

I believe by analyzing the log data within a SIEM, I would be able to corroborate my initial conclusion with additional facts on whether the activity was malicious. 

I believe I would be able to determine if any devices in the client's network were compromise by analyzing the log data with a SIEM 

 

S4 Is this investigation related to any other previous OR ongoing investigations? If so: identify and cite the previous OR ongoing investigations.

 

This investigation has no relationship to any other previous or ongoing investigation that I am aware of.

 

 

BACKGROUND
The BACKGROUND section describes in greater detail the information you were given prior to beginning your investigation. Enrich the information about the instigating incident by determining the information can be gathered from logs or people about what might have led up to the incident. 

BACKGROUND should contain NONE of your conclusions or findings determined after actually beginning your investigation. All investigation findings belong in the ASSESSMENT section.

B1 What is the date and time[range] of the reported incident? Be sure to include the timezone.

Date: 12/06/2017

Time: 18:34:24 GMT - 18: 35: 33 GMT

 

B2 What exactly is the task that has been assigned to you? (What must you determine before your investigation can be considered completed?)

I am tasked with assessing whether the attack is malicious by scrutinizing the PCAP, and then validating these preliminary conclusions through an analysis of log data in the SIEM.

 

B3 Who assigned investigation of this incident to you?

Virgil

 

B4 What sources of evidence were you given access to in order to conduct your investigation? (An older SBAR? SIEM logs? PCAP? Memory image? Forensic disk image? The ability to interview specific employees? If you have been given access to it during your investigation, make it clear here!)*

* If any of your provided evidence sources feature only evidence from a particular timestamp or date||time range, this is the place to make note of it.

I have been provided with PCAP and SIEM logs as the sources for this investigation.

The SIEM log was captured on 12/06/2017 from 1800GMT - 1900 GMT

The PCAP was captured on 12/06/2017 and spans from 18;34:19. 962565 - 18:35:47.958228

 

 
ASSESSMENT
The ASSESSMENT section contains "answers" to all the outstanding questions your investigation was tasked with addressing.

This is usually the meatiest part of the report: you are presenting the bulk of your investigation findings in this section, providing the final analysis & implications of the information that was gathered during the course of the investigation. Remember: as an analyst, it is your job to connect all the dots based on the evidence you are able to dig up; if you describe a specific detail or event, ensure you are making it clear why you are including that information. What is its meaning||significance||implications? Your answers should clearly include this context about the information you are providing.

Details about the specific evidence you discovered that supports the findings you describe here should be included in the TECHNICAL APPENDIX; the answers here should only include findings you were able to determine from the examination of that evidence during the course of your investigation.

A1 ANY CORRECTIONS TO MAKE TO INFO REPORTED IN S OR B? • Did you discover that any founding hypotheses reported in the SITUATION or BACKGROUND section were incorrect? If so: you should state explicitly what you determined to be incorrect, along with the relevant corrected information.

 

The notions that the incident was a remote intrusion activity came up not torue after the investigation. The investigation revealed that the attack originated internally and not externally.

A2a WHAT HAPPENED • How did this take place? (What tool(s) or technique(s) caused the incident to occur?)

There was a brute-force attack where an LAB-Kali(10.5.10.105)(made several attempts to log into WordPress instance account on the server LAB-Web02(10.5.20.16) by using Hydra.

 

A2b WHAT HAPPENED • What is the full date||time range of the entire incident? Are there distinct timeranges that define specific "clusters" of activity? At what particular timestamps did important events occur at?

 12/06/2017 6:14:43 - 6:18:58   First cluster of Brute Force activity <LAB-Kali.at.USA.co> 10.5.10.105 uses Hydra to Brute-Force the authentication form from wp-login.php account hosted by LAB-W02

LAB-kali' is the attacking device because it is the device where a malicious entity is performing actions intended to compromise or exploit vulnerabilities in another device or system. This device could be running software tools designed for penetration testing and cyber attacks, such as Kali Linux, hence the 'kali' in its hostname. Kali Linux comes with numerous built-in tools that can be used for purposes like password cracking, network scanning, and vulnerability exploitation.

'LAB-Web02', on the other hand, is the web server hosting a WordPress instance. WordPress is a widely used content management system that allows users to build and manage websites. In this scenario, 'LAB-Web02' is the target of the attack being carried out by 'LAB-kali'.

 12/06/2017 6:15:07 LAB-Kali (10.5.10.105) made the first successful authentication: unknown credentials

12/06/2017 6:27 - 6:36PM the second cluster of Brute-Force activity by LAB-Kali was unleashed on LAB-Web02 to access the authentication credentials of it WordPress instance account

 12/06/2017 6:34:45 LAB-Kali (10.5.10.105) made second successful authentication: credentials given by Wireshark as user id == admin, pwd == Winter2017wp@dmin 

12/06/2017 6:46 - 6: 51 PM The third cluster of Brute-force attacked from LAB-Kali.at.USA.co on LAB-Web02 to authenticate the login credentials of the WordPress login account was recorded.

 12/06/2017 6:47:02 LAB-Kali (10.5.10.105) made third successful authentication into the WordPress login account: unknow credentials

 12/06/2017 6:50:01 LAB-Kali (10.5.10.105) made the fourth successful authentication; credentials unknown

 

A2c WHAT HAPPENED • What actually happened during this incident? This should be a description of the sequence of events that occurred during this incident, listed in chronological order. This should be one of the lengthier answers in your SBAR!

 
During the incident, the primary security breach was a brute-force attack. An attacker (WEB.Kali.at.USA.co) aimed to access the authentication details of AT-USA's WordPress instance hosted on the LAB-Web02 server. In simpler terms, the attacker was attempting to "break into" the system by trying all password combinations until they found the right one.

This occurred on 12/06/20.

Our analysis pinpointed the attack's origin to a host server, LAB.Kali.at.USA.co, with an IP address of "10.5.10.105", which utilized Hydra to initiate the Brute-force attack.

The attacker (LAB-Kali) specifically targeted AT-USA's WordPress instance on the LAB-Web02 server, IP "10.5.20.16". This server was primarily attacked, facing numerous login attempts by the assailant.

Here's a breakdown of the attack sequence:

6:14:43 - 6:18:58: Initial brute-force activity. LAB-Kali.at.USA.co (IP 10.5.10.105) employed Hydra to brute-force wp-login.php on LAB-W02.

12/06/2017 6:15:07: LAB-Kali's first successful login; exact credentials remain unidentified.

12/06/2017 6:27 - 6:36PM: LAB-Kali initiated a second brute-force wave on LAB-Web02.

12/06/2017 6:34:45: LAB-Kali's second successful entry used credentials: Username - "admin", Password - "Winter2017wp@dmin".

12/06/2017 6:46 - 6:51PM: LAB-Kali launched a third brute-force attempt on LAB-Web02.

12/06/2017 6:47:02: LAB-Kali's third successful login, but credentials remain unknown.

12/06/2017 6:50:01: LAB-Kali's fourth successful entry; credentials are still unidentified.

LAB-Kali achieved their goal, compromising the WordPress account by obtaining its credentials on four distinct occasions. They gained access using the credentials: Username - "admin", Password - "Winter2017wp@dmin".

Our research suggests that the attacker repeatedly succeeded in accessing AT-USA's WordPress account on the LAB-Web02 server for the same purpose: to obtain login details.

Certain vulnerabilities in the WordPress account allowed the attacker unauthorized access. This weak point was the main entryway for the attacker.

The attacker executed multiple brute-force assaults on the WordPress account, consistently obtaining authentication details.

Our findings highlight that brute-force was the consistent technique across all successful breaches. This suggests the attacker's keen interest in accessing the WordPress admin account.

A4b SCOPE • Which internal hosts were involved? Be sure to list the role that each internal device played in this incident. Include both hostname and IP address whenever possible.
1. Internal Host Name: LAB-Web02(10.5.20.16): This was the webserver the attacker repeatedly tried to log into by Brute-Force method

2. Internal Hostname: Lab.Kali.at-usa.co. (10.5.10.105) Attacker's hostname and IP

 

 

 

A4c SCOPE • Were any users OR services OR devices compromised? If so: describe what, exactly, was compromised...& what caused the compromise?

After repeated login attempts the username and password of the WordPress admin login form was authenticated successfully by the Hydra attacker (10.5.10.106) showing brute-force attack thereby compromising the WordPress instance account.

A4d SCOPE • Which external hosts were involved? Be sure to list the role that each external host played in this incident. Include both resolved domain name and IP address whenever possible.

After the investigation it was deduced that there was no external host in this incident, rather the attacker was an internal player.

 

A5a SEVERITY • How serious is this incident? Assess the severity of the incident by taking into consideration factors like whether anything of potential value was compromised, and how much this incident disrupted normal business functioning.

This incident was severe in that the login credentials of our client's WordPress instance account had been accessed by an attacker.

 

A5b SEVERITY • Of the compromised users OR services OR devices, were any of particular value to an attacker? This answer should address whatever you described in the answer to Were any users OR services OR devices compromised?.

Yes. Administrative privileges to LAB-Web02 server seemed to be of particular interest to the attacker. However, it is  unknown if any relevant documents were stolen from the server per this investigation other than the WordPress account credentials.

 

A5c SEVERITY • Did $whatever_was_compromised have access to $anything_of_value?

It is not known as of now. However, LAB-Web02 server might contain important information such as employee account information, company files belonging to AT-USA, our client

 

A5d SEVERITY • Was $anything_of_value stolen||exfiltrated during this incident?

No evidence to support this claim now except the login credentials.

 

A6a INCIDENT RESPONSE (SO FAR) • Has the threat been contained?

Yes, because we are not seeing the repetition of the same event in the server since the last WordPress instance login was completed

 

A6b INCIDENT RESPONSE (SO FAR) • To your knowledge, were any immediate mitigations put into place?

No evidence to support this claim 

 
RECOMMENDATION
The RECOMMENDATION section is where you reflect on how the organization might prevent incidents like this from happening in the future—be proactive! Be forward-thinking!

Always explicitly state your reasoning for making a particular recommendation.

REMEMBER:
• You must always make a cost||benefit analysis when considering recommendations—prioritize solutions that offer the greatest coverage for the least amount of effort. The amount of effort required by the organization to implement a suggestion should absolutely be justified by the degree of protection undertaking such an implementation would afford. Your recommendations are only as valuable as they are realistic to actually implement.
• Be sure to include sufficient information about each recommendation so that if another employee were tasked with implementing your recommendations, they will not need to do any additional research in order to implement your suggestion. If you're recommending that additional research into determining a viable specific solution be made, that should be stated explicitly.
• Do not make generic security recommendations that are NOT related to what occurred during this incident; each recommendation you make should be obviously related to something that is involved in the incident you are writing this SBAR about.

 

INCIDENT RESPONSE||TRIAGE
Try to include some immediate incident response triage recommendations. What immediate recommendations would you make to help contain the incident and prevent it from potentially escalating in SEVERITY &&|| SCOPE?

R1a INCIDENT RESPONSE||TRIAGE • Should any devices be considered compromised and quarantined and/or reimaged? If so: list each, describing what exactly should be done.

1. I recommend that the LAB-Web02 be disconnected, forensically imaged and examined and be reset to a good state to prevent further potential attack.

2. The attacker's device with the hostname Lab.kali.at-usa.co (10.5.10.105) should be quarantined for further digital analysis.

 

R1b INCIDENT RESPONSE||TRIAGE • Should any credentials be reset? If so: belonging to which user(s) and/or services?

All user credentials associated with the WordPress site should be reset

Existing account holders should be verified to ensure that they are rightful owners of their respective accounts

The webmaster WordPress login account password should be reset.

 

R1c INCIDENT RESPONSE||TRIAGE • Should any devices be singled out for additional analysis? (Should any logs be gathered from a particular device?) If so: be sure to specify which device(s), what evidence you would want to access on each device, and what unanswered||remaining||open questions examining this additional evidence would help you resolve.

The compromised server should be singled out for additional analysis.

Additional logs should be gathered from any of the devices involved in the attack, particularly the authentication logs from the WordPress instance hosted on LAB-Web02. This will help in determining which other user credentials were also compromised.

The attacker's device should be singled out for additional analysis. We will want to know if any confidential data was transferred from the server 

 

R1d INCIDENT RESPONSE||TRIAGE • Do any employees need to be questioned? If so: whom, and regarding what? What unanswered||remaining||open questions would interviewing this employee help you resolve?

Yes. 

1. The employee who owns the device, Lab.kali.at-usa.co(10.5.10.105) will have to answers question based on the attack

2. The LAB-Web02 administrator will have to answer questions about the attack and explain to us whether the WordPress site has any information of value to the attacker.

These employees will help to understand the motive and purpose of the attack

R1e INCIDENT RESPONSE||TRIAGE • Does anybody—people or companies—need to be notified about this compromise or breach? If so: whom, and what exactly do they need to be informed about?

 AT-USA Management should be notified

Employees whose accounts would be reset should be notify as well

 

R1f INCIDENT RESPONSE||TRIAGE• Do any new investigations need to be started? If you discovered any potentially suspicious activity that turned out to not be related to your current investigation, be sure to specify here.

No

 

R1g INCIDENT RESPONSE||TRIAGE • Should any old or ongoing investigations be amended with corrected information discovered during this investigation? If this investigation is related to a another investigation and you were able to determine any of the other investigation's findings were incorrect, specify what needs to be amended here.

The title of the investigation should be Internal intrusion attempt since it has been discovered that the attacker is an insider on the same network.

 

PREVENTION OF FUTURE INCIDENTS OF THIS TYPE
In your ASSESSMENT section, you should have identified  in A3 (What vulnerable services or threat vectors were taken advantage of during this incident?)—whatever you identified in answering that question...you want to make remediation recommendations, whenever possible, on how to better protect that threat vector from being abused again in the future. What options does the client have when it comes to deciding how to prevent these in the future?

R2a PREVENTION • Can you recommend any changes that could be implemented within the company's internal infrastructure that would actively prevent another attack like this from succeeding in the future?

1. I recommend all users create complex and unique passwords. For instance, must include lower and uppercase letters as well as numbers and special characters

2. I recommend implementation of account lockout policies. After a certain number of failed login attempts, the account should be either temporarily locked or the user should be forced to wait a longer period between each login attempt. 

3. I also recommend the company should adopt Two-Factor Authentication policies for all users

4. I recommend the use of firewall rules, Intrusion Detection Systems (IDS), and Intrusion Prevention Systems (IPS) to detect and block repeated login attempts from the same IP address.

R2b PREVENTION • Can you think of any changes that could be made to the company's standard internal policies might better protect the company's infrastructure from being so vulnerable to this type of attack?

The company should consider a policy to Monitor failed login attempts and set up alerts for multiple failed login attempts in a short period of time. This can help you quickly detect and respond to brute force attacks. 

 

TECHNICAL APPENDIX
The TECHNICAL APPENDIX is where you "show your work" for the findings you have described in detail in the ASSESSMENT section.

REMEMBER:
• The potential reader of this SBAR is likely distracted and strapped for time—if they need to dig into the technical details of your analysis, they should be able to reproduce your results that led you to your conclusions using the details you include in your TECHNICAL APPENDIX. Keep the SBAR clear and concise by providing answers that are easily grasped even if your reader is scanning your report quickly for relevant information.
• All information required to reproduce your findings reported in the SBAR proper should be included here. If you were to need to replicate your investigation findings a year from now (after you've forgotten all the details yourself), what technical details would you want to have provided here to help save you time replicating your original findings? That's exactly what should be included here.
• Feel free to include Splunk search result URLs for valuable search queries, but if you do: clearly describe why the search was valuable so that nobody has to click it, load it, and then guess how it is relevant.

An attacker operating from the host Lab.Kali.at-usa.co (IP address 10.5.10.105) initiated a brute force attack on our server LAB-Web02 (IP address 10.5.20.16) in an attempt to obtain login credentials to a WordPress account, employing the tool Hydra.

The first cluster of this brute force activity was observed on 12/06/2017, between 6:14:43 and 6:18:58. The attacking device with IP 10.5.10.105 was seen using Hydra to force the authentication credentials of a wp-login.php account on the LAB-Web02 server.

At 6:15:07 on the same day, the attacker from 10.5.10.105 was able to achieve the first successful authentication, though the credentials used remain unknown.

At 6:34:45, a second successful authentication was made by the attacker. The credentials were identified by Wireshark as: User ID - admin, Password - Winter2017wp@dmin.

The attacker made a third successful entry into the WordPress login account at 6:47:02, but again, the credentials remain unknown.

Finally, at 6:50:01, the attacker from 10.5.10.105 made the fourth successful authentication, with the specific credentials remaining unknown.

 

1. SPL: (index="web_apache" clientip="10.5.10.105" host="LAB-Web02" source="access.log" sourcetype=access_combined status=302 | reverse) This is a valuable search query because it shows all the four successful login attempts by the attacker within the selected time range.

2. index="web_apache" method IN (POST, GET) | reverse. This is essential because it filters the time range from the beginning of the attack to the end.</p>
