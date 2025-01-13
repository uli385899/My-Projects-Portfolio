# Home Security Information and Event Management (SIEM) Lab

This project involves setting up a home SIEM (Security Information and Event Management) lab on my Kali Linux machine, designed to monitor and analyze system activity by forwarding all logs and events to the Elastic Cloud server. The goal of this lab is to provide real-time security monitoring, log aggregation, and threat detection in my local environment.

<details>
  <summary>Getting Started</summary>

  ## Setting up the environment

  <table>
  <tr>
    <td><img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-1.png" alt="SIEM Image 1" width="1000"/></td>
    <td><img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-6.1.png" alt="SIEM Image 2" width="1000"/></td>
  </tr>
</table>

To set up the lab, the Elastic Defend agent was added as an integration on the Elastic Cloud platform. The integration process involved copying the installation commands provided by Elastic into the terminal on my local machine. These commands installed and configured the Elastic Agent, enabling it to collect and forward system logs, security events, and other telemetry data from my local host to the Elastic Cloud server.

  ## Verifying intergration

<img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-4.1.png">
<img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-5.1.png">
  
To verify that telemetry data was being successfully forwarded from my local machine to the Elastic Cloud server, an nmap scan was executed. This generated system events and logs related to the scan. Verification was performed by navigating to the Discovery tab in Elastic Defend, conducting a quick KQL search query for "nmap".

  <hr>
</details>

<details>
  <summary>Creating a dashboard</summary>

  ## Importance of creating a dashboard

Creating visualizations for ingested data is essential for monitoring trends, identifying anomalies, and gaining actionable insights. Dashboards allow for real-time tracking of log inflow and make it easier to interpret large datasets visually.

  ## My created dashboard

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-7.png">

 
This visualization, titled "Logs Inflow," represents the number of logs recorded every 30 minutes on my local machine. The horizontal axis displays the timeline (@timestamp) in 30-minute intervals, while the vertical axis shows the count of records during each interval. The area chart provides an intuitive view of log volume trends, enabling quick identification of spikes in activity.

I used the KQL (Kusto Query Language) tool to search for _**process.args : "nmap"**_, filtering the data to reduce the number of records from thousands to just a few dozen. This approach makes the results more focused and actionable by narrowing down to relevant insights, which can later be used for different queries.

  ## My dashboard's visual configuration

<table style="width: 100%; text-align: center; border-collapse: collapse;">
  <tr>
    <!-- Top Row: SIEM-8 and SIEM-10 -->
    <td style="width: 50%; padding: 10px;">
      <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-8.png" 
           alt="SIEM Image 8" 
           style="width: 100%; height: auto;">
    </td>
    <td style="width: 50%; padding: 10px;">
      <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-10.png" 
           alt="SIEM Image 10" 
           style="width: 100%; height: auto;">
    </td>
  </tr>
  <tr>
    <!-- Bottom Row: SIEM-9 -->
    <td colspan="2" style="padding: 10px;">
      <div style="display: flex; justify-content: center;">
        <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-9.png" 
             alt="SIEM Image 9" 
             style="width: 50%; height: auto;">
      </div>
    </td>
  </tr>
</table>

<hr>
</details>

<details>
  <summary>Creating rules</summary>

  ## The purpose of creating rules in SIEM systems

  Rules in SIEM systems play a critical role in detecting, monitoring, and responding to security threats. They analyze ingested data in real-time to identify suspicious activities, such as brute force attacks, unauthorized access, or data exfiltration attempts. When specific conditions or patterns are met, rules trigger alerts that are sent to analysts for immediate action. This helps reduce incident response times, cut down on noise, and ensures security teams focus on actionable threats.

  ## Nmap scanning detection rule
  
  In this rule, I configured the SIEM to detect any nmap scan executed on my local host by monitoring command-line arguments and specific event actions. When such activity is identified, the rule triggers an alert and sends a detailed notification via email. This rule helps ensure timely awareness of potential reconnaissance activities on the system.

<hr>
<img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-11.png">

We begin by defining the rule using a Custom Query type, selecting the relevant data view (logs-*), and constructing a query to detect nmap activity. The query, _**process.args : "nmap" or event.action : "nmap_scanning" and host.name : "kali"**_, filters logs to identify events where nmap scans are executed on the local host. To minimize duplicate alerts, suppression fields like _**Effective_process.entity_id**_ and _**Effective_process.name**_ are added, and the rule is set to trigger once per execution within a 5-minute window.

<hr>
<img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-12.png">

Next, we configure the basic details of the rule by providing a title and a description that outlines its purpose. The severity level is set to **Low** since nmap scans are typically reconnaissance activities performed for information gathering rather than overtly malicious actions

The risk score is assigned a value of **50**, indicating a moderate level of concern. This score helps define how impactful the event could be on the host, balancing between informational and actionable risk.

Finally, tags such as **nmap**, **reconnaissance**, and **localhost** are added to categorize the rule. These tags make it easier to filter and identify the type of alert triggered, streamlining future investigations and reports.

<hr>
<img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-13.png">

In this step, we configured the schedule for the rule to ensure timely detection of nmap scans. The rule is set to run every **1 minute**, enabling near real-time monitoring for any matching events. Additionally, the look-back time of **1 minute** is configured to ensure no events are missed during execution intervals. This scheduling ensures the rule captures and alerts nmap scans promptly, providing quick notifications for immediate action.

<hr>
<img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-14.png">

Finally, we configure the **action** to be taken when the rule's conditions are met. In this case, the SIEM is set to send an email notification using the preconfigured Elastic-Cloud-SMTP connector. The email contains a clear subject, _**"Alert: Nmap Scan Detected on Localhost"**_, and a concise message stating that an nmap scan has been detected and immediate action is required. This ensures that any suspicious activity is promptly communicated for further investigation or response.

<hr>
</details>

<details>
  <summary>Testing our set rule</summary>

  ## Performing an nmap scan to trigger an alert

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-15.png">

  We now will proceed to perform a basic nmap scan on the localhost using the command _**sudo nmap -A -sV localhost**_. This action will generate logs that match the conditions defined in the "**Nmap Scan Detection on localhost**" rule, allowing us to test if the SIEM successfully detects the scan and triggers an alert.

  ## Receiving alert via SIEM

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-17.png">

  As shown here, the alert was successfully triggered at the correct **timestamp**, matching the conditions set in the rule. Additionally, key information such as _**host.name**_, _**process.name**_, _**process.args**_, and _**user.name**_ is provided, giving analysts a clear overview of the event. This information is vital for conducting further investigations and ensuring that the activity is understood and addressed appropriately.

  ## Receiving alert via email

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/siem-16.png">

  Additionally, the alert notification was successfully received via email, as configured in the **action** step of the rule. The email promptly informs the recipient that an nmap scan was detected on the localhost, allowing for immediate awareness and action.

  <hr>
</details>

## Conclusion

From completing this lab, I gained valuable hands-on experience in the following areas:  
- **Data Aggregation and Centralization:** Understanding how to collect, organize, and centralize logs from multiple sources into a SIEM.  
- **Visualization Creation:** Developing intuitive dashboards to track and analyze log data effectively.  
- **Log Analysis:** Interpreting patterns and trends in log data to identify anomalies or spikes in activity.  
- **Configuration and Customization:** Configuring specific parameters, such as time intervals and data filters, to meet targeted analytical needs.  
- **Alert Rule Creation:** Designing and implementing custom rules for generating alerts based on specific log patterns or anomalies, enhancing proactive threat detection.

This lab is just the beginning of my journey in leveraging SIEMs to enhance security within my virtualized network. By applying these skills, I plan to build more advanced monitoring solutions, refine detection mechanisms, and continually improve the security posture of my virtualized environments.

[Go back to Main repository](https://github.com/uli385899/My-Projects-Portfolio)
