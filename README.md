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

  
</details>

[Go back to Main repository](https://github.com/uli385899/My-Projects-Portfolio)
