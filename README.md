<h1>AWS VPC Flow Logs</h1>

<h2>Description</h2>
We've acquired Alpha Inc.'s AWS VPC flow logs from 2023-09-28. This is the day we discovered malicious activity targeting the company's Wordpress web server. The logs have been copied into your VM in the directory /sec401/labs/1.3/20230928. Let's take an initial look at the acquired logs.
<br />


<h2>Objectives</h2>

- <b>Observe traffic summaries from AWS cloud instances</b> 
- <b>Identify outlier conversations</b>
- <b>Compare and contrast observations with captures viewed in tcpdump and Wireshark<b>

<h2>Environments Used </h2>

- <b>Linux</b> (Slingshot)

<h2>Program walk-through:</h2>

<p align="center">
Use "ls" to list all files and directories in /sec401/labs/1.3/20230928: <br/>
<img src="https://imgur.com/8RQArbl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
Command line notes:<br/>
 - "ls" will list each item in the directory <br />
 - "| wc -l" uses a pipe (|) to direct output from the previous command into the wc command to count lines (-l) <br />
<br />
<img src="https://imgur.com/BlyzQ8Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
 What type of file format are the flow logs stored in? Note that the file extension is usually a good indicator, <br/> but how can you verify the file type in Linux to be sure? Let's use the command file on one of the files to check. <br/>
<br />
<img src="https://imgur.com/l8SwQCm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Confirm your selection:  <br/>
<img src="https://imgur.com/8RaVtAB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://imgur.com/ua5RtQE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Sanitization complete:  <br/>
<img src="https://imgur.com/jCG9fZa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/5qhF0oq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/AjTYQJo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/d2eLsUD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/ICZUjJ5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/PEjFB5s.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/41tCWOi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/IjFcqcz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/OChZSd7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
