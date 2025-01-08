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
<summary>Total Recorded Alerts</summary>
  
  ## Total Recorded Alerts

  <hr>

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/nmap-easy-7.png">
  By the end of our scan, we managed to reduce the number of alerts to just 22. This number could have been further minimized had I avoided performing the initial ping scan or a full preliminary scan. Nonetheless, this represents less       than 25% of the maximum alert threshold our target would have permitted before terminating our efforts.

  <hr>

</details>

<details>
  <summary>Lab Conclusion</summary>
  
  ## Lab Conclusion

  <img src="https://github.com/uli385899/My-Projects-Portfolio/blob/main/.assets/nmap-easy-8.png">
  This lab provided an excellent opportunity to practice Nmap techniques while maintaining a low detection profile in an environment with active firewall, IDS, and IPS defenses. By strategically selecting scan options and prioritizing       stealth, I was able to successfully identify the operating system of the target machine while keeping intrusion alerts well below the maximum threshold.
  <p>&nbsp;</p>
  The results highlight the importance of thoughtful reconnaissance planning, such as limiting unnecessary scans and focusing only on relevant ports and services. The adjustments I made to reduce alerts demonstrate the value of iterative    learning and adaptive strategies in penetration testing.
  <p>&nbsp;</p>
  Overall, this exercise reinforced the critical balance between achieving technical objectives and minimizing detection, an essential skill for ethical hacking and cybersecurity professionals.
  
</details>

[Go back to Nmap Evasion Labs Branch](https://github.com/uli385899/My-Projects-Portfolio/tree/Nmap-Evasion-Labs)

[Go back to main](https://github.com/uli385899/My-Projects-Portfolio/tree/main)
