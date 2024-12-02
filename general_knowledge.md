# General Knowledge

## Pyramid of Pain

The Pyramid of Pain is a conceptual model developed by security expert David J. Bianco to illustrate the impact of disrupting different types of adversary indicators in cybersecurity. It organizes indicators of compromise (IOCs) into six levels based on the difficulty for defenders to detect and the level of pain it causes attackers when these indicators are disrupted.

1. Hash Values (Trivial) - a value that uniquely identifies data; can help identify malware samples, malicious/suspicious files, etc.

2. IP Address (Easy) - can be used to block, drop, or deny inbound requests from specific addresses.

3. Domain Names (Simple) - domains will be more challenging to change than IP addresses, but is still doable.

4. Network Artifacts (Annoying) - Adversaries’ network activities that are observable. This includes exact C&C protocol to destination network resource, URI patterns, C2 information embedded in network protocols, distinctive HTTP User-Agent, or SMTP Mailer values.

5. Host Artifacts (Annoying) - Specific observables on one or more endpoint/host devices. This includes changes to registry keys or values known to be created by specific pieces of malware, files or directories dropped in certain places or using certain names, names or descriptions or malicious services.

6. Tools (Challenging) - Artifacts of tools (e.g. DLLs or EXE names or hashes) that the attacker is using. This includes software adversary uses to accomplish their mission, e.g., Tor, Windows Task Scheduler, GCC, PowerShell, etc.

7. TTPs (Tough) - The overall methods and approaches used by attackers to achieve their goals. Disrupting TTPs requires attackers to rethink their entire strategy, causing the highest level of pain and disruption.

## Cyber Kill-Chain

A model developed by Lockheed Martin to describe the stages of a cyberattack, providing a framework for understanding the various phases an attacker goes through when executing a cyberattack. It helps organizations identify potential weaknesses in their defense strategy and better respond to intrusions.

1. Reconnaissance - discovering and collecting information on the victim. Considered the planning phase. Includes OSINT - open source intelligence.

2. Weaponization - the creation of a malicious payload, often combining a remote access tool with a exploit.

3. Delivery - the attacker delivers the weaponized exploit to the target, typically via email, web applications, or other methods.

4. Exploitation - the exploit is triggered allowing the attacker to gain access to the target system, often by exploiting a vulnerability.

5. Installation - malicious software is installed on the target system, often establishing persistence for future attacks.

6. Command & Control - The attacker establishes communication with the compromised system to send commands or exfiltrate data.

7. Actions on Objectives - attacker achieves their final goal which could be data theft, system disruption, or other malicious objectives.
