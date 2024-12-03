# Security +

# I. Today's Security Professional

## Objectives of Cybersecurity

The basic objectives of cybersecurity are confidentiality, integrity, and availability of your operations (the CIA triad). Security incidents occur when there is a breach of these security controls.

### The CIA Triad

- `Confidentiality` concerns itself with ensuring unauthorized individuals are not able to access sensitive information. This is achieved with security controls (firewalls, access control, encryption, etc.).

- `Integrity` ensures there are no unauthorized modifications to information or systems (intentionally or unintentionally).

- `Availability` - ensures information and systems are available for users at the time of request. This is achieved with controls such as fault tolerance, clustering, backups, etc.

### Nonrepudiation

`Nonrepudiation` is not part of the triad, but is important as it means that when someone performs some action, they cannot later deny having taken that action. These include digital signatures or some type of history monitoring.

### The DAD Triad

The DAD triad explains the three key threats to cybersecurity efforts, which are disclosure, alteration, and denial. These map directly to one of the goals of cybersecurity.

- `Disclosure` is the exposure of information to unauthorized individuals (`data loss`). It is a violation of confidentiality. `Data exfiltration` is the removal of sensitive information. This can also happen accidentally.

- `Alteration` is the unauthorized modification of information and the violation of integrity.

- `Denial` is the disruption of an authorized user's access to information.

### Breach Impact

A security incident can impact an organization in several different ways. Risk can cross into more than one of the following categories.

- `Financial Risk` is monetary damage (destruction, loss of information, trust/business).

- `Reputational Risk` involves negative publicity, loss of goodwill among customers, employees, etc.

- `Strategic Risk` the organization becomes less effective in meeting its major goals and objectives through loss of product, IP, etc. This risk is concerned with the very existence of an organization and its ability to execute its business plans.

- `Operational Risk` is the ability to carry out day to day functions. This is more focused on inefficiency and delays within the organization.

- `Compliance Risk` occurs when a breach causes a break in regulatory requirements (HIPPA, etc). This leads to sanctions and fines.

## Implementing Security Controls

An organization implements security controls to preserve the CIA triad. `Control Objectives` are statements of a desired security state an organization wishes to achieve. `Security Controls` are the actual measures that fulfill these security objectives.

### Gap Analysis

`Gap Analysis` are conducted to evaluate security controls. It is a review of control objectives and an examination of the controls designed to achieve those objectives. If there is a instance where a control does not meet the objective, there is a `gap`. These gaps should be treated as potential risks and remediated.

### Security Control Categories

There are four categories for security controls based on how they meet their objective.

- `Technical controls` - enforce the CIA triad via digital space (firewall rules, access control).

- `Operational controls` - the processes put in place to manage technology in a secure manner (user access reviews, log monitoring, vulnerability management).

- `Managerial controls` - the mechanics of the risk management process (periodic risk assessments, security planning exercises).

- `Physical controls` - fences, lighting, locks, fire suppression system, alarms.

### Security Control Types

Security controls are also divided into types based on their desired effects.

- `Preventive controls` intend to stop a security issue before it occurs (firewalls and encryption).

- `Deterrent controls` prevent an attacker from attempting to violate a security policy (guard dogs or security).

- `Detective controls` identify security events that have already occurred (IDS).

- `Corrective controls` remediate security issues that have already occurred (restoring backups after an attack).

- `Compensating controls` are designed to mitigate risk associated with exceptions made to a security policy.

- `Directive controls` inform employees and others what they should do to achieve security objectives (policies and procedures).

## Data Protection

Data exists at three main states.

- `Data at rest` is data stored on hard drives, tapes, in the cloud, etc. Prone to theft by insiders or external attackers who gain access.

- `Data in transit` is data that is in motion/transit over a network. At risk especially over untrusted network.

- `Data in use` is data that is actively in use by a system.

Different security controls can be applied to help safeguard data in all of these states.

### Data Encryption

Use encryption to prevent information being exposed.

### Data Loss Prevention

DLP systems help enforce policies and procedures to prevent loss / theft. These search systems for sensitive information. `Agent-based DLP` uses software agents installed on systems that search those systems for sensitive information. Can also monitor system configuration and user actions, blocking undesirable actions (blocking USBs). `Agentless (network-based) DLP` systems sit on the network and monitor out-bound network traffic. These watch for unencrypted transmissions, blocking them.

DLP systems use `pattern matching`, watching for telltale signs of sensitive information (credit card numbers, socials). They also use `watermarking`, where electronic tags are applied to sensitive documents which the system monitors for (unencrypted content containing those tags) (think DRM).

### Data Minimization

Data minimization techniques seek to reduce risk by reducing the amount of sensitive information that we maintain on a regular basis. Destruction of data no longer needed is best. `Deidentification` is the process that removes the ability to link data back to an individual, reducing sensitivity. `Data obfuscation` is the process of transforming data into a format where the original information cant be retrieved. Data obfuscation includes:

- `Hashing` which uses a function to transform a value in a dataset to a corresponding hash value. Vulnerable to a `rainbow table attack` where a attacker computes hashes of candidate values and checks them to see if those hashes exist in the file.
- `Tokenization` replaces sensitive values with a unique identifier using a lookup table (this needs to take into account securing the lookup table).
- `Masking` partially redacts sensitive information by replacing some or all sensitive fields with blank characters (think credit cards).

### Access Restrictions

`Access restrictions` are security measures that limit the ability of individuals or systems to access sensitive information or resources.

- `Geographic restrictions` limit access to resources based on the physical location of the user or system.
- `Permission restrictions` limit access based on the user's role or level of authorization.

### Segmentation and Isolation

Access can be limited by placing sensitive systems on different parts of the network. `Segmentation` places sensitive systems on separate networks where they can still communicate with each other but have severe restrictions. `Isolation` goes further by completely cutting off access to outside networks.

## Summary

1. The three core objectives of cybersecurity are confidentiality, integrity, and availability.
2. Nonrepudiation prevents someone from denying that they took an action.
3. Security controls may be categorized based on their mechanism of action and their intent.
4. Data breaches have significant and diverse impacts on organizations.
5. Data must be protected in transit, at rest, and in use.
6. Data loss prevention systems block data exfiltration attempts.
7. Data minimization reduces risk by reducing the amount of sensitive information that we maintain.

a, b, c, b, d, d, b, a, d, a, c, a, d, d, d, a, c, b, a, a

d, b, c, b, d, d, b, a, d, a, c, a, d, d, d, a, c, b, a, a

# II. Cybersecurity Threat Landscape

## Exploring Cybersecurity Threats

Threat actors come in various levels of skills and capabilities.

### Classifying Cybersecurity Threats

There are several characteristics which can be used to differentiate between the types of threat actors.

`Internal vs External` - threats can also come from within the organization.
`Level of Sophistication / Capability` - threat actors vary greatly in their level of cybersecurity sophistication and capability.
`Resources / Funding` - funding can range from organized crime / government sponsorship to hobbyists with no funding.
`Intent / Motivation` - from simple thrills to corporate espionage to political objectives.

They types of 'hats' attackers wear vary.

`White-hat` hackers or authorized hackers are those that act with authorization to discover vulnerabilities.
`Black-hat` hackers are those with malicious intent.
`Gray-hat` hackers are those who fall somewhere in between.

### Threat Actors

- `Unskilled Attackers` or `script kiddie` are those that use hacking techniques but have limited skill. They rely on automated tools they download from the internet. They are generally less discriminating in their targeting selections. Motivation is based on proving their skill.

- `Hacktivists` use hacking techniques to accomplish some activist goal. They believe they are motivated by the greater good. They are more motivated than unskilled attackers and may even risk getting caught to get their goals (this may be a badge of honor). Skill varies widely, but there is reason to believe some are actual cybersecurity professionals, posing a significant danger. Resources can vary significantly as well (Anonymous is an example). These can be internal actors that disagree with their companies policies (government employees, whistleblowers)(think Edward Snowden).

- `Organized Crime` appears when there is money to be made. The common thread in these groups is motivation and intent (illegal financial gain). There is usually no political type motivation and these organizations tend to stay in the shadows. They are active in many sectors: - cyber-dependent crime - child sexual abuse material - online fraud - dark web - cross-cutting crime factors
  Organized crime is usually moderately skilled to highly skilled. Resources are bigger in terms of time and money.

- `Nation-State Attackers` may be state sponsored. `Advanced Persistent Threats` applies here. Nation-States are able to use advanced techniques, stay persistent in their attacks over a significant amount of time, and continued attacks for possibly years. Hackers are highly skilled with significant resources. Motivation is both political and / or economic. `Zero-day` attacks are often used, vulnerabilities that have not been patched nor are known about.

- `Insider Threat` attacks occur when an employee, contractor, vendor, or other individual with authorized access to information and systems uses that access to wage an attack against the organization. Can be of any skill level. Motivations can vary greatly. They often work alone with limited financial backing. Behavioral assessments are powerful tools against insider attacks. `Shadow IT` is a threat here - employees using technology services that are not approved by their organization (usually without malicious intent).

- `Competitors` may engage in corporate espionage.

### Attacker Motivations

Primary motivations behind cyber attacks include:

- `Data exfiltration` - motivated by the desire to obtain sensitive or proprietary information.
- `Espionage` - attacks motivated by organizations seeking to steal secret information.
- `Service disruption` - attacks seek to interrupt critical networks (banking).
- `Blackmail` - attacks to extort money or other concessions.
- `Financial gain` - attacks motived by desire to make money.
- `Philosophical/political belief` - ideology or political reasons.
- `Ethical attacks` - desire to expose vulnerabilities and improve security.
- `Revenge` - get even with an organization or for retribution.
- `Disruption/chaos` - basic desire to cause chaos.
- `War` - disrupt military operations or affect the outcome of a armed conflict.

### Threat Vectors and Attack Surfaces

Attackers must find a means to an organizations information or systems. First, they need an `attack surface` - a system, application, or service that contains a vulnerability to exploit. Then, they must get access by exploiting one of those vulnerabilities using a `threat vector`. Threat vectors are the means that threat actors use to obtain access.

Security professionals are tasked with reducing the size and complexity of the attack surface.

- `Message-Based Threat Vectors` - Email is the most commonly exploited threat vector. Success only needs to occur once in order to launch a broader attack. Attacks are not limited to email and can come through `SMS` or `IM`. Voice calls are another approach for vishing attacks. Social media is another approach to harvest information for use in other attacks.
- `Wired Networks` - Gaining access to a orgs physical location. This can happen by them gaining access to a lobby and working on their laptops while connected to a wall jack. Or they can access a unsecured device.
- `Wireless Networks` - unsecured or poorly secured wireless networks pose significant risk; this also includes bluetooth-enabled devices.
- `Systems` - vulnerable software, unpatched operating systems, credentials that were never changed, legacy applications that are no longer supported.
- `Files and Images` - files with embedded malicious code that activates a malware infection upon opening; often sent via email or placed somewhere.
- `Removable Devices` - usb drives left in parking lots loaded with malware that launches when plugged in.
- `Cloud` - any cloud services with security flaws, accidentally published API keys/passwords.
- `Supply Chain` - attacking hardware, software, or service providers. This can include interfering with hardware/software in transit to the target.
