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

<h3>Task 1: VPC Flow Log Format</h3>
<br/>

<p align="center">
Use "ls" to list all files and directories in /sec401/labs/1.3/20230928: <br/>
<img src="https://imgur.com/8RQArbl.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
1. List the available files and then determine how many log files are there in the flow logs directory. <br/>
<br/>
 Command line notes:<br/>
 - "ls" will list each item in the directory <br />
 - "| wc -l" uses a pipe (|) to direct output from the previous command into the wc command to count lines (-l) <br />
<br />
<img src="https://imgur.com/BlyzQ8Q.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<br />
2. What type of file format are the flow logs stored in? Note that the file extension is usually a good indicator, <br/> but how can you verify the file type in Linux to be sure? Let's use the command "file" on one of the files to check. <br/>
<br />
<img src="https://imgur.com/l8SwQCm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
3. Now review the contents of the file. To avoid too much data on the screen, we'll output just the first 4 lines of the file 222677128680_vpcflowlogs_us-east-2_fl-0272f423386e6eaaf_20230928T2355Z_e92fb168.log.gz. <br/>
<br/>
Command lines <br/>
zcat /sec401/labs/1.3/20230928/222677128680_vpcflowlogs_us-east-2_fl-0272f423386e6eaaf_20230928T2355Z_e92fb168.log.gz | head -4 <br/>
<br/>
Command line notes: <br/>
 - zcat will concatenate (cat) a gzip-compressed file <br/>
 - head -4 prints the first 4 lines of input <br/>
 <br/>
<img src="https://imgur.com/8RaVtAB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
<h3>Task 2: Flow Record Fields</h3
<br/>
<p align="center">
The VPC flow logs are text-based files containing long tables of connection data. The first line of each file includes the header row. It indicates the type of data stored in each space-separated column. The remaining rows are the connection data. Here's a brief explanation of each field in the flow records table.
Wait for process to complete (may take some time):  <br/>
 <br/>
<img src="https://imgur.com/ua5RtQE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
1. Determine the total number of flow records in the collection of log files. Remember to subtract 1 for each log file to account for the header rows.
<br/>
<br/>
Command lines
<br/>
Use zcat to extract all the files at once and simultaneously perform a line count across the data of all the extracted files:
<br/>
zcat /sec401/labs/1.3/20230928/*.log.gz | wc -l
<br/>
<br/>
Command line notes: <br/>
 - *.log.gz uses the asterisk * wildcard to specify all files ending .log.gz as input to the calling command (zcat)
 <br/>
 <br/>
<img src="https://imgur.com/jCG9fZa.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
2. We discovered in Labs 1.1 and 1.2 an attacker IP address of 20.106.124.93 targeting a Wordpress web server. Let's filter the logs to create a new log file with flows from only that IP address to make analysis easier.
<br/>
 <br/>
Command lines: <br/>
Like most things on the Linux command line, there are multiple ways to accomplish the task. One option is to use zcat again and pipe the output to grep to filter for the IP address. grep is a very powerful command for data filtering. Instead, let's combine those steps by using the zgrep command and output the filtered results to a new file named attacker-flows.log in the directory /sec401/labs/1.3:
<br/>
<br/>
zgrep --no-filename 20.106.124.93 /sec401/labs/1.3/20230928/*.log.gz > /sec401/labs/1.3/attacker-flows.log
<br/>
<br/>
Command line notes: <br/>
 - zgrep is a wrapper around grep with the added ability to directly search gzip-compressed files. <br/>
 - The --no-filename parameter prevents zgrep from prepending each matched line with the filename it came from. <br/>
 - The use of > redirects the output of the command on the left to the file on the right.
 <br/>
 <br/>
<img src="https://imgur.com/5qhF0oq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
 How many flow records included the attacker's IP?
<br/>
<br/>
Command lines <br/>
  - wc -l /sec401/labs/1.3/attacker-flows.log
<br/>
<br/>
<img src="https://imgur.com/AjTYQJo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
<br />
 <h3>Task 3: Review the Attacker's Flow Data</h3
<br/>
<p align="center">
1. Based on the available log data, at what time did the attacker's first connection begin?
<br/>
<br/>
Command lines <br/>
<br/>
To find the start time that any particular connection began, we can use the start value from the log. Note from the Flow Record Fields table above, the start field is in the 15th column. Since the timestamps are stored in Unix epoch time, which is the number of seconds since January 1, 1970, the smaller the value the number it is, the earlier in time it is. We can therefore use the sort command to sort numerically on column 15 by adding the parameter -nk 15. Since it will be thousands of records, pipe the results through head -1 to get the first result, which is the time the first connection began. 
<br/>
<br/>
sort -nk 15 /sec401/labs/1.3/attacker-flows.log | head -1
<br/>
<br/>
Command line notes: <br/>
 - It's often possible to combine command parameters in front of a single dash as we've done above. In other words, -nk 15 is the equivalent of -n -k 15
<br/>
<br/>
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
