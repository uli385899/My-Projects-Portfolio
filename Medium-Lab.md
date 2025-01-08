# Medium Difficulty - Nmap Firewall/IDS/IPS Evasion Lab

In this lab, the same client wants to know if I could find the target's DNS server version. Submitting the banner as the answer.

<details>
  <summary>Getting Started</summary>
  
  ## Getting Started

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/nmap-medium-9.png">
  
  Just like in the [Easy Lab](https://github.com/uli385899/My-Projects-Portfolio/blob/Nmap-Evasion-Labs/Easy-Lab.md), I connected to the same company's network using the OpenVPN configuration file from the previous lab and verified the connection by successfully pinging the host.

<hr>

</details>

<details>
<summary>Initial Scan</summary>
  
  ## Initial Scan

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/nmap-medium-8.png">
 
 Since we know we need to find DNS server information, we can narrow our port search to port 53. This significantly reduces the number of alerts to be recorded, allowing more focus and resources for enumeration and analysis.
 
  - **Pn**: Disables pinging of hosts.
  - **n**: Disables DNS resolution.
  - **disable-arp-ping**: Disables checking if the target's IP address corresponds with a MAC address.
  - **max-retries**: Specifies the maximum number of connection retries for each port.
  - **packet-trace**: Similar to a packet sniffer, this option shows the results of sent and received network packets.
  - **stats-every**: Displays scan progress at intervals by set time.
  - **T**: Adjusts the aggressiveness of the scan (3 being normal or default).
  - **p**: Specifies the port(s) to be scanned.
  - **oN**: Saves scan in nmap formation.
  - **reason**: Provides additional details about the response or lack of response from a target, explaining why Nmap categorized a port as it did.

## Initial Scan Results

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/nmap-medium-7.png">
  
  Examining the **no-response** in the scan results, it appears that the target's Firewall or IDS/IPS is intercepting and dropping our SYN packet requests. Since we know the port and service exist, we'll need to devise a clever method to bypass these defenses and ensure the requests are accepted.  

  <hr>

</details>


<details>
<summary>Evasion Scan</summary>
  
  ## UDP Scan

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/nmap-medium-5.png">
  
 In the initial scan, I didn’t specify the type of scan, so Nmap defaulted to a **TCP SYN** scan (equivalent to using the -sS option). This likely caused the target’s defenses to filter out the packets, as DNS (port 53) typically operates over TCP only in specific scenarios-- such as zone transfers or handling large responses.

To address this, I made a single modification to the initial scan by adding the **-sU** option to perform a UDP scan. The results, along with the packet trace, showed that the target opened up and responded to the request, in contrast to filtering or ignoring it.

  <hr>

</details>

<details>
  <summary>Service Scan</summary>

  ## Service Scan

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/nmap-medium-4.png">
  
  I again modified the scan with its last addition with using a service scan (-sV) on top of UDP.

  ## Service Scan Results

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/nmap-medium-3.png">

  The service version running on the DNS server is the banner, that being a HTB flag.

  <hr>
  
</details>

<details>
  <summary>Total Alerts Recorded</summary>

  ## Total Alerts

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/nmap-medium-2.png">
  
  Starting from the pings to verify our host was responding to the three different nmap scans, I managed to be under 75 alerts before being blocked from the defenses. I'd say it was a pretty successful testing!
  
</details>

<details>
  <summary>Lab Conclusion</summary>

  ## Lab Conclusion

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/nmap-medium-1.png">
  
  This lab emphasized the importance of the passive reconnaissance phase, as failing to get it right initially cost me hours of troubleshooting-- even caused the target to block me due to the excessive number of scans performed. Conducting thorough research on the target before initiating active scans can provide a significant advantage. A well-thought-out plan is far more efficient than attempting to improvise during an ongoing process.

Throughout the lab, I had to draw heavily on my foundational knowledge of network protocols and learn how defensive systems respond to improperly configured scans. While the process itself was straightforward, overlooking key details or misconfiguring scan parameters can quickly lead to frustration, second-guessing, and unnecessary delays.

Ultimately, this experience reinforced a critical lesson: it’s not just about what you know, but about recognizing and addressing what you don’t yet know.

<hr>
  
</details>

[Go back to Nmap Evasion Labs Branch](https://github.com/uli385899/My-Projects-Portfolio/tree/Nmap-Evasion-Labs)

[Go back to main](https://github.com/uli385899/My-Projects-Portfolio/tree/main)
