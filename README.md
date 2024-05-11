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
Launch the utility: <br/>
<img src="https://imgur.com/8RQArbl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select the disk:  <br/>
<img src="https://imgur.com/BlyzQ8Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Enter the number of passes: <br/>
<img src="https://imgur.com/l8SwQCm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://imgur.com/8RaVtAB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://imgur.com/ua5RtQE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://imgur.com/jCG9fZa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/5qhF0oq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/AjTYQJo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/d2eLsUD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/ICZUjJ5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/PEjFB5s.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/41tCWOi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://imgur.com/IjFcqcz.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br /
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
