# Day 3: Advanced Endpoint Protection, EDR & Host Firewalls

[https://www.youtube.com/live/_aixWwgrQPU](https://www.youtube.com/live/_aixWwgrQPU)

## Introduction Summary

Day 3 emphasizes advanced security controls including proper logging with Sysmon, advanced endpoint protection evaluation, host-based firewalls for lateral movement prevention, and threat emulation testing. The session demonstrates how Windows authentication is fundamentally clear-text, making lateral movement trivial without proper controls. Key focus areas include using tools like Atomic Red Team to test EDR capabilities, implementing host-based firewalls to break lateral movement chains, and understanding that EDR is critical but not sufficient alone. The instructor stresses the importance of fundamental knowledge over tool-specific skills and shares insights about career development and community building in cybersecurity.

## Key Takeaways

### 1. **Windows Authentication is Fundamentally Insecure**

- Windows NTLM authentication (v1, v2) is essentially clear-text authentication
- Challenge-response mechanism allows password hash extraction from network traffic
- Pass-the-hash attacks work because Windows accepts hash values as authentication
- Host-based firewalls are the most effective defense against lateral movement

### 2. **EDR is Critical but Not Sufficient Alone**

- EDR provides the broadest coverage against MITRE ATT&CK techniques
- Every security technology can be bypassed - defense in depth is essential
- Many EDRs detect suspicious activity but don't generate high-priority alerts
- Regular testing with tools like Atomic Red Team is essential for validation

### 3. **Proper Logging Strategy Fundamentals**

- Sysmon provides superior Windows logging in a single command deployment
- Default Windows event logging is "absolute garbage" for security analysis
- Sigma rules provide cross-platform detection logic for multiple SIEMs
- Focus on actionable logs that enable incident response, not just volume

### 4. **Community and Continuous Learning Philosophy**

- Share knowledge freely rather than hoarding it for perceived job security
- Help desk and SOC Level 1 positions provide excellent foundational learning opportunities
- Focus on fundamentals (TCP/IP, command line, networking) over specific tool training
- Building trust through consistent knowledge sharing creates long-term professional success

## Complete Study Notes

### Advanced Logging with Sysmon

**Sysmon Implementation and Benefits**

- Single command deployment: `sysmon64.exe -accepteula -i config.xml`
- Uses Swift on Security or Olaf Hartthog configurations for optimal coverage
- Provides detailed process execution logging with command lines, hashes, parent processes
- Logs appear in Applications and Services > Microsoft > Sysmon > Operational
- Captures network connections, file modifications, registry changes, and process creation

**Comparison to Windows Default Logging**

- Default Windows event logs focus on application performance, not security events
- Command line execution not logged by default in Windows
- Enabling Windows command line logging requires complex multi-step configuration
- Event Viewer contains mostly meaningless technical details rather than actionable security data
- Sysmon immediately provides security-relevant logging without complex configuration

**Sysmon Log Analysis Examples**

- Process creation events show executable path, command line arguments, and parent process
- Network connection events reveal external communications and potential C2 traffic
- File modification events track malware persistence and system changes
- Registry modification events detect configuration changes and malware installation

### Advanced Endpoint Protection and EDR

**EDR Capabilities and Limitations**

- Provides broadest coverage across MITRE ATT&CK framework techniques
- Most powerful single security control but not sufficient alone
- Can be bypassed by sophisticated attackers (BHIS, Trusted Sec, Red Siege can bypass any EDR)
- Many products detect suspicious activity but categorize it as low-priority alerts
- Target breach example: FireEye detected the attack but didn't generate critical-level alerts

**EDR Market and Business Considerations**

- Major vendors: CrowdStrike, SentinelOne, Carbon Black (now VMware), Cylance (acquired by BlackBerry)
- BlackBerry sold Cylance to White Wolf Security for ~$140M after buying it for $1.4B (90% loss)
- Market consolidation continues with acquisitions and technology integration
- Cost considerations require balancing security needs with budget constraints

**Velociraptor for Incident Response**

- Free, open-source endpoint visibility and collection tool
- Used extensively by BHIS for incident response engagements
- Enables remote forensic data collection across multiple endpoints simultaneously
- Provides hunt capabilities and artifact collection without installing permanent agents
- Complements traditional EDR solutions for investigation and response activities

### Host-Based Firewalls and Lateral Movement Prevention

**Windows Authentication Weaknesses**

- NTLM authentication sends challenge-response in clear text over network
- 16-byte challenge sent in clear, wrapped with password hash using known algorithm
- No salting in Windows password hashing (only LM and NT hash types exist)
- NTLMv3 is authentication protocol, not hashing protocol - still vulnerable to interception
- Responder tool can intercept and extract password hashes from LLMNR/NBT-NS traffic

**Pass-the-Hash Attack Mechanics**

- Attacker gains access to one system and dumps password hashes
- Hash values can be used directly for authentication without cracking passwords
- Works because Windows accepts hash as valid authentication credential
- Enables rapid lateral movement across environments with shared service accounts
- LAPS (Local Administrator Password Solution) helps but doesn't eliminate the issue

**Host-Based Firewall Implementation**

- Windows built-in firewall is "horrible" but better than nothing
- Can be configured via Group Policy for centralized management
- Block workstation-to-workstation communication while allowing server access
- Create rules allowing server subnets to communicate with workstations
- Many AV products include superior firewall management capabilities

**Network Segmentation Strategy**

- Treat internal network as hostile environment (Starbucks analogy)
- Systems should be more secure internally than at public WiFi locations
- Segment all the way down to desktop level when possible
- Use private VLANs, network access control, or host-based firewalls
- Design architecture assuming compromise will occur - focus on containment

### Threat Emulation and EDR Testing

**Atomic Red Team Implementation**

- Developed by Red Canary for MITRE ATT&CK technique testing
- PowerShell-based framework for executing specific attack techniques
- Available in Lima Charlie dashboards for integrated testing
- Provides expected outputs and detection signatures for each test
- Can be installed with single PowerShell command for rapid deployment

**Blue Spawn as EDR Testing Platform**

- Open-source EDR-like tool used for testing and demonstration
- Limited MITRE coverage compared to commercial EDR solutions
- Useful for understanding detection principles and testing methodologies
- Demonstrates difference between detection and alerting priorities
- Shows importance of tuning and signature quality over quantity

**Testing Methodology Best Practices**

- Run EDR in "alerting non-blocking mode" during testing
- Avoid disabling security controls completely during evaluation
- Focus on detection capabilities rather than blocking functionality
- Test both automated tools (Atomic Red Team) and manual techniques (Metasploit)
- Document gaps and plan remediation for undetected techniques

**Signature Development Considerations**

- Avoid writing signatures specific to testing tools (don't detect "atomic red team" directory)
- Focus on generic behavioral patterns rather than tool-specific indicators
- Example: detect regsvr32 with specific switches rather than test framework paths
- Balance specificity to avoid false positives while maintaining broad coverage
- Regular testing ensures signatures remain effective against evolving threats

### Professional Development and Career Guidance

**Fundamental Skills vs. Tool Knowledge**

- TCP/IP three-way handshake understanding more valuable than specific tool training
- Command line proficiency (Windows and Linux) essential for all security roles
- Tools change every 5 years - fundamentals remain constant across decades
- College graduates often lack practical skills despite theoretical knowledge
- Industry needs candidates with solid fundamentals, not just certifications

**Entry-Level Career Paths**

- Help desk provides exposure to wide variety of technologies and problems
- SOC Level 1 offers introduction to security tools and incident response
- Network Operations Center (NOC) builds strong networking foundations
- Cloud support roles increasingly valuable and future-proofed
- Extract maximum learning from entry-level positions through active engagement

**Sigma for Cross-Platform Detection**

- Acts as "Rosetta Stone" for detection rules across multiple SIEM platforms
- Write once, deploy to Splunk, Elastic, ArcSight, and other platforms automatically
- YAML-based rule format with MITRE ATT&CK technique mapping
- GitHub repository contains extensive rule library for common attack patterns
- Essential skill for detection engineers and threat hunters

**Community Engagement and Knowledge Sharing**

- Share knowledge freely rather than hoarding for perceived job security
- Social media sharing helps build professional reputation and network
- Teaching others reinforces your own knowledge and skills
- Avoid "sheeple" mentality that looks down on non-technical people
- Building trust through giving creates more opportunities than taking

## Quiz Questions

1. **Question**: Explain why Windows NTLM authentication is considered "clear-text" despite using password hashes, and how this enables pass-the-hash attacks.
    - **Answer**: Windows NTLM authentication is considered clear-text because the entire authentication exchange happens in the clear over the network. The process works as follows: (1) Client attempts to authenticate, (2) Server sends a random 16-byte challenge in clear text, (3) Client wraps their password hash (not password) with this challenge using a well-known algorithm and sends the response in clear text. Since there's no salting and the algorithm is known, an attacker can intercept this traffic and reverse-engineer the password hash from the challenge and response. Pass-the-hash attacks work because Windows accepts the hash value itself as valid authentication - attackers don't need to crack the password, they can use the intercepted hash directly to authenticate to other systems in the environment.

2. **Question**: What is the "Starbucks analogy" for host-based firewalls, and why does this highlight a fundamental problem with internal network security?
    - **Answer**: The Starbucks analogy points out that computers are more secure at a coffee shop than on their own corporate network. At Starbucks, systems don't trust the network or other computers, so they enable firewalls and security controls. However, on internal corporate networks, systems act like "that annoying uncle who unbuttons his pants after Thanksgiving dinner" - they assume they're "home" and can relax all security controls. This creates a situation where systems communicate freely with each other, enabling rapid lateral movement for attackers. The analogy highlights that internal networks should be treated as hostile environments with the same security posture as public WiFi networks, using host-based firewalls to prevent workstation-to-workstation communication while still allowing necessary server access.

3. **Question**: What is the most important characteristic of an effective EDR, and why is EDR alone insufficient for organizational security?
    - **Answer**: EDR is the single most powerful security control because it provides the broadest coverage across MITRE ATT&CK framework techniques - appearing in most defensive cards in the "Back Doors and Breaches" game. However, EDR alone is insufficient because: (1) Every security technology can be bypassed by sophisticated attackers (BHIS, Trusted Sec, Red Siege can bypass any EDR), (2) Many EDRs detect suspicious activity but categorize it as low-priority rather than critical alerts, missing actual incidents, (3) Defense in depth requires overlapping fields of visibility - when one control fails, others must detect the attack. The instructor emphasizes that while EDR is without question one of the most important tools in an environment, treating it as the only necessary security control leads to false confidence and organizational vulnerability.

4. **Question**: What does it mean by "defense in depth" versus "depth of money," and how should organizations properly implement layered security?
    - **Answer**: "Defense in depth" means overlapping fields of visibility where each security control supports the others - if AV fails, network monitoring detects the attack; if EDR is bypassed, host firewalls contain lateral movement. However, many organizations implement "depth of money" instead - spending large amounts on single solutions (like EDR on every system) or buying multiple expensive tools without proper integration. True defense in depth requires: (1) UEBA for behavioral analysis, (2) Endpoint protection for host-based detection, (3) Network security monitoring for traffic analysis, (4) SIEM for log correlation, (5) Host-based firewalls for lateral movement prevention. Each component should be designed to detect what others might miss, creating structural integrity where no single point of failure leads to complete organizational compromise. The goal is architectural design that assumes compromise will occur and focuses on detection and containment rather than prevention alone.

## Notable Quotes

> "If you build your entire life around using a tool, that tool will find a way to replace you."
> 

> "Everything can and will be bypassed. Every single technology that you use in your organization can and will be bypassed."
> 

> "Your EDR is without question your single most powerful tool in your environment. It's not your only tool."
> 

> "You should never be in a situation where you're making judgments about the intelligence of people and you should always be going out to try to bring the fire of learning."
> 

> "Smart people don't share because they're trying to hold on to that knowledge because that knowledge is their self-worth and they have this fear that if they share that knowledge with the world that somehow their overall personal value is going to be less."
> 

> "Blue team is faster. Blue team all day... Blue team is very much like English - it is an easy language to get into and you can barely get by and you can be functional, but to master it is incredibly difficult."
> 
