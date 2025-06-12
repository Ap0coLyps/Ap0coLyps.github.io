## How botnets communicate and How to catch them.

A botnet is a network of compromised computers or devices — often referred to as "bots" or "zombies" that are remotely controlled by an attacker, usually without the device owners' knowledge. These bots are typically used for malicious purposes such as DDoS attacks, spam campaigns, data theft, or malware distribution.

Antivirus software on hosts can remove the malware when detected, but detection is not always guaranteed. In this blog, I want to explore the possibility of detecting bots within a network by analyzing network traffic data.

---

### How do bots stay hidden within network traffic?

Just like botnets try to stay under the radar of antivirus software, bots also attempt to hide within normal network traffic to avoid detection. To catch them, it's crucial to understand how they remain hidden. 

Bots need to communicate with a central server, known as a Command and Control (C2) server, to receive instructions on what actions to perform. To obtain these instructions, bots must establish some form of connection with the C2 server to check for commands. This communication needs to happen consistently to ensure timely execution.

This behavior is known as beaconing, and it can be configured to occur as frequently as every 10 seconds for rapid response, or as infrequently as once per day when stealth is a priority.

![image](https://github.com/user-attachments/assets/704b762b-e916-4e1f-a113-dff67af4d3c1)


#### Some T-SQL Code

```tsql
SELECT This, [Is], A, Code, Block -- Using SSMS style syntax highlighting
    , REVERSE('abc')
FROM dbo.SomeTable s
    CROSS JOIN dbo.OtherTable o;
```

#### Some PowerShell Code

```powershell
Write-Host "This is a powershell Code block";

# There are many other languages you can use, but the style has to be loaded first

ForEach ($thing in $things) {
    Write-Output "It highlights it using the GitHub style"
}
```
