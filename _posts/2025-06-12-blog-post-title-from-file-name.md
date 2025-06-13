## How botnets communicate and How to catch them.

A botnet is a network of compromised computers or devices — often referred to as "bots" or "zombies" that are remotely controlled by an attacker, usually without the device owners' knowledge. These bots are typically used for malicious purposes such as DDoS attacks, spam campaigns, data theft, or malware distribution.

Antivirus software on hosts can remove the malware when detected, but detection is not always guaranteed. In this blog, I want to explore the possibility of detecting bots within a network by analyzing network traffic data.

---

### How do bots stay hidden within network traffic?

Just like botnets try to stay under the radar of antivirus software, bots also attempt to hide within normal network traffic to avoid detection. To catch them, it's crucial to understand how they remain hidden. 

Bots need to communicate with a central server, known as a Command and Control (C2) server, to receive instructions on what actions to perform. To obtain these instructions, bots must establish some form of connection with the C2 server to check for commands. This communication needs to happen consistently to ensure timely execution.
This behavior is known as beaconing, and it can be configured to occur as frequently as every 10 seconds for rapid response, or as infrequently as once per day when stealth is a priority.

Here is an example of beaconing detected using WireShark with a 10-second interval from my test setup, which uses HTTP for communication.

![image](https://github.com/user-attachments/assets/704b762b-e916-4e1f-a113-dff67af4d3c1)

Jittering is a technique used by bots to make their communication patterns less predictable. Instead of connecting to the command and control (C2) server at fixed intervals (like exactly every 10 seconds), bots will add a random delay — for example, between 8 and 12 seconds.
This randomness makes it harder to detect beaconing patterns, which often rely on spotting regular, repeating traffic.

A bot will rarely communicate directly with its Command and Control server. It may use techniques like DNS or IP spoofing to make the traffic appear as if it's going somewhere else. Therefore, detecting a large amount of recurring traffic from a machine in a LAN to a C2 server is often not straightforward.

This IP spoofing can be observed when looking at the network traffic, so thats what i'm going to do.

---

### Test setup

The Botnet
I deployed a test botnet using Covenant, a .NET-based Command and Control (C2) framework. Covenant allows you to generate payloads (bots) and provides a user-friendly interface for managing them. Since it is designed for testing purposes, it does not include antivirus evasion. Therefore, antivirus protection must be disabled on the target system for successful deployment.

You can find the project on GitHub: https://github.com/cobbr/Covenant

The Firewall:
The firewall is going to be pfSense wich is an open-source firewall platform based on FreeBSD. It provides advanced network security features such as firewall rules, NAT, VPN support, traffic shaping, intrusion detection, and logging — all through an easy-to-use web interface. And it is free!

Detection and visualisation:
For this project, I’ll be using the Elastic Stack (formerly known as ELK Stack), which consists of Elasticsearch, Logstash, and Kibana.

    Elasticsearch is a powerful search and analytics engine that stores and indexes large volumes of data.

    Logstash is used to collect, parse, and transform logs before sending them to Elasticsearch.

    Kibana provides a visual interface to explore and analyze the data through dashboards and graphs.

This stack is ideal for detecting patterns in network traffic and visualizing potential indicators of botnet activity.


#### Some PowerShell Code

```powershell
Write-Host "This is a powershell Code block";

# There are many other languages you can use, but the style has to be loaded first

ForEach ($thing in $things) {
    Write-Output "It highlights it using the GitHub style"
}
```
