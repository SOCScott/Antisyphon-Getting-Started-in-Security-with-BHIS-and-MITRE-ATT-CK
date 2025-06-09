# Day 2: Egress Traffic Analysis, UEBA, and Strategic Logging

# Day 2: Egress Traffic Analysis, UEBA & Logging

## Introduction Summary

Day 2 focuses on advanced network threat detection and User Entity Behavioral Analytics (UEBA), moving beyond traditional signature-based detection to mathematical and behavioral analysis. The session covers egress traffic analysis using tools like Zeek and Rita for beacon detection, the critical importance of proper logging strategies, and why Windows default event logging is inadequate for security analysis. The instructor emphasizes that with encrypted traffic becoming standard, organizations need mathematical approaches to identify command & control patterns, comprehensive log correlation across multiple sources, and proper tuning mindset rather than expecting AI to automatically solve security problems.

## Key Takeaways

### 1. **Signature-Based Detection is Dead**

- Traditional signature-based detection fails against encrypted HTTPS/TLS traffic
- TLS/SSL interception products don't solve the problem because attackers use double encryption
- Modern attacks require mathematical and heuristic analysis instead of pattern matching
- Need to move toward behavioral analysis and statistical anomaly detection

### 2. **Mathematical Network Analysis Works**

- Rita uses beacon detection based on interval timing, data size, and connection duration
- K-means clustering algorithms identify C2 patterns regardless of encryption
- High beacon counts (100K+ connections) vs. normal traffic (20-80 beacons) indicate compromise
- Mathematical analysis can detect patterns that signature-based tools miss completely

### 3. **UEBA Requires Human Intelligence and Tuning**

- No single log tells the complete story - requires correlation across multiple data sources
- "False positives" don't exist - only detection tuning opportunities that improve understanding
- Industry has set the bar too low for AI, making security professionals replaceable
- Proper tuning builds deep network knowledge and makes analysts more valuable

### 4. **Logging Strategy Must Focus on Value, Not Volume**

- Most organizations collect massive amounts of useless log data (terabytes daily)
- Only 5-10% of security detections actually come from logs despite huge collection efforts
- Windows default event logging is "absolute garbage" for security analysis
- Tools like Sysmon provide actionable security logging in a single command deployment

## Complete Study Notes

### Egress Traffic Analysis Fundamentals

**The Problem with Traditional Detection**

- Signature-based detection relies on pattern matching inside traffic content
- Encryption (HTTPS/TLS) makes signature detection impossible
- TLS/SSL interception products fail because sophisticated attackers use double encryption
- Need mathematical approaches that work regardless of encryption

**Network vs. Endpoint Protection**

- Gartner agrees: endpoint protection alone is insufficient
- IoT devices, shadow IT, and embedded systems can't run EDR solutions
- Network-level analysis catches attacks that bypass endpoint protection
- Examples: Mr. Robot Raspberry Pi drop box, camera system compromises leading to ransomware

**Moving Beyond Signatures**

- Traditional approaches look for specific byte patterns or signatures
- Modern approaches use statistical analysis and behavioral patterns
- Mathematical models can identify command & control regardless of encryption method
- Focus on metadata and traffic characteristics rather than content

### Zeek Network Analysis Platform

**What Zeek Does**

- Creates separate log files for different network protocols (DNS, HTTP, connections, etc.)
- Generates metadata about network traffic rather than storing raw packets
- Provides consistent timestamping across all log types
- Huge customer base with extensive community support

**Zeek vs. NetFlow**

- NetFlow is Cisco-created standard that became industry de facto
- Other vendors created competing standards (JFlow, SFlow, TFlow, QFlow)
- Different implementations make analysis difficult across multi-vendor environments
- Zeek provides standardized logging format regardless of underlying network equipment

**Zeek Implementation Options**

- Can be deployed on dedicated network capture hardware
- Works with Windows Subsystem for Linux (WSL2) for endpoint analysis
- Microsoft integration available but requires expensive E5 licensing
- WSL2 trick: shared Ethernet interface allows full packet capture on Windows endpoints

### Rita (Real Intelligence Threat Analytics)

**Rita Background and Philosophy**

- Free tool for automated beacon detection using mathematical analysis
- Named after instructor's mother who fought cancer; kept free per her wishes
- 26+ patents but committed to remaining free for the cybersecurity community
- AC Hunter provides GUI web interface for Rita's mathematical engine

**Beacon Detection Mathematics**

- Based on Plato's Theory of Forms - identifying "perfect" beacon characteristics
- Three key characteristics analyzed: interval timing, data size, connection duration
- Uses K-means clustering algorithms to identify patterns in network traffic
- "Flux capacitor" visualization - closer to center indicates more perfect beacon

**Understanding Beacon Patterns**

- Perfect beacons score close to 1.0 with high connection counts
- Normal network traffic shows 20-80 beacons with lower scores
- Compromised systems show 100K+ beacons with near-perfect scores
- Accounts for network variance using statistical clustering (MADMA algorithm)

**Long Connection Analysis**

- "Spaghetti string" analogy - reassembles fragmented communications over time
- Attackers may randomize individual connection sizes but total duration reveals C2 pattern
- 24-hour communication sessions identified regardless of individual connection fragmentation
- Complements beacon detection for comprehensive command & control identification

**Real-World Examples**

- TeamViewer breach detection through beacon analysis
- Hospital Gillette RDP compromise identification
- Dragon Naturally Speaking customer service backdoor detection
- LAN Turtle USB-to-Ethernet devices with embedded Linux kernels

### User Entity Behavioral Analytics (UEBA)

**The Multi-Source Correlation Challenge**

- Single event: user logs into domain controller
- Multiple log sources tell the story: Sysmon, Event Viewer, NetFlow, cameras, switches, DHCP, web proxy, Exchange/O365
- No single log provides complete narrative - requires correlation across sources
- UEBA fuses multiple data sources to create comprehensive user behavior baseline

**Mathematical Approaches to UEBA**

- "Stacking cards" methodology: +1 for login, -1 for logoff, threshold-based alerting
- AI learns normal behavior patterns and alerts on statistical deviations
- Edward Snowden example: normal system admin access vs. massive data download anomaly
- Uses algorithms like K-means clustering, MADMA, Bayesian analysis

**The "False Positive" Fallacy**

- Instructor's philosophy: no such thing as "false positives," only "detection tuning opportunities"
- Calling them false positives psychologically shifts blame to vendor
- Proper approach: tune alerts for legitimate use cases rather than disabling them
- Examples: service accounts, help desk users, vulnerability scanners, backup systems

**Why Tuning is Critical**

- Manual tuning builds deep understanding of network environment
- Industry has set bar too low, expecting AI to solve everything automatically
- This mindset makes security professionals replaceable by automation
- Proper tuning differentiates skilled analysts from button-pushers

**Common Tuning Scenarios**

- SVC accounts logging into hundreds of systems: create exception for specific service account from specific source
- Help desk users accessing 20+ systems: create rule for help desk personnel
- Vulnerability scanner generating alerts: exception for scanner account and source system
- Working through 200-400 "false positives" is manageable with systematic approach

### Logging Strategy and Implementation

**The Logging Volume Problem**

- Organizations focus on log volume (terabytes/day) rather than value
- Largest BHIS customer logs 1 petabyte daily but can't answer basic questions
- Only 5-10% of security detections actually come from logs despite massive collection
- "Logging industrial complex" drives unnecessary volume increases for vendor profit

**Windows Default Logging Problems**

- Windows event logs provide minimal security-relevant information
- Event Viewer contains mostly application performance data, not security events
- Command line execution not logged by default
- Enabling Windows command line logging requires complex multi-step configuration process

**Critical Event IDs for Windows**

- 4624: Successful logon
- 4625: Failed logon
- 4634: Logoff
- 4768: Kerberos authentication ticket (TGT) requested
- 4769: Kerberos service ticket requested
- 4776: Domain controller attempted to validate credentials

**Sysmon: The Superior Solution**

- Single command deployment: `sysmon.exe -accepteula -i config.xml`
- Provides detailed process execution logging with command lines, hashes, parent processes
- Swift on Security and Olaf Hartthog configurations provide excellent starting points
- Logs appear in Applications and Services > Microsoft > Sysmon > Operational
- Dramatically superior to Windows default event logging for security analysis

**Advanced Network Logging Concepts**

- Sensor placement: pre-NAT for proper host visibility
- Full PCAP vs. metadata trade-offs (portability vs. storage requirements)
- Dedicated capture hardware (Gigamon, Coralight) vs. open source solutions
- JA3/JA4 TLS fingerprinting for analyzing encrypted connections
- User agent string analysis for identifying suspicious or unique clients

## Quiz Questions and Answers

### Question 1: Why does traditional signature-based detection fail for modern network traffic analysis, and what mathematical approach does Rita use to solve this problem?

**Answer:** Signature-based detection fails because modern attacks use encrypted HTTPS/TLS traffic, making content inspection impossible. Even TLS/SSL interception products fail because sophisticated attackers employ double encryption or additional encoding/obfuscation. Rita solves this using mathematical analysis of beacon characteristics - specifically interval timing, data size, and connection duration. Using K-means clustering algorithms, Rita identifies command & control patterns regardless of encryption by analyzing metadata rather than content. Perfect beacons cluster near a score of 1.0 with high connection counts (100K+ vs. normal 20-80), making encrypted C2 traffic mathematically identifiable.

### Question 2: What is the John Strand’s philosophy about "false positives" in UEBA systems, and why does he believe this mindset is critical for cybersecurity professionals?

**Answer:** The instructor argues there are no "false positives," only "detection tuning opportunities." When an alert triggers (like an account logging into hundreds of systems), the alert is working correctly - it's detecting abnormal behavior as designed. Calling them false positives psychologically shifts blame to the vendor and leads to alerts being disabled rather than properly tuned. The correct approach is creating exceptions for legitimate use cases (service accounts, help desk users, vulnerability scanners). This tuning process is fundamental to the analyst's job and builds deep network understanding. The instructor warns that expecting AI to automatically handle this makes security professionals replaceable, as the industry has "set the bar so low" for automation.

### Question 3: Describe the "spaghetti string" analogy for long connection analysis and explain how it helps detect command & control traffic.

**Answer:** The "spaghetti string" analogy explains how Rita detects fragmented command & control communications over time. Like breaking a dry spaghetti string into various sized pieces (some long, some short, some medium), attackers may randomize individual connection sizes to evade detection. However, when you reassemble all the pieces, the total length remains the same. Rita analyzes all connections between two systems over extended periods (like 24 hours). Regardless of whether individual connections are tiny, large, or mixed sizes, the total communication duration reveals the persistent C2 channel. This mathematical approach identifies long-term compromise even when attackers attempt to disguise traffic patterns through connection fragmentation.

### Question 4: Why does the instructor consider Windows default event logging "absolute garbage" for security analysis, and how does Sysmon solve these problems?

**Answer:** Windows default event logging fails because it focuses on application performance rather than security events. Critical security activities like command line execution aren't logged by default, and enabling them requires complex multi-step configuration processes involving audit policies, registry settings, and group policy modifications. The instructor notes he's been doing cybersecurity for 25 years and still can't understand most Windows event log entries, which focus on meaningless technical details rather than actionable security information. Sysmon solves this with single-command deployment (`sysmon.exe -accepteula -i config.xml`) that immediately provides detailed process execution logging including command lines, file hashes, parent processes, and user context - all the information needed for effective security analysis and incident response.

## Notable Quotes

> "There's no such thing as false positives... there are detection tuning opportunities."
> 

> "Logs are an absolute train wreck. There is no 'you've been hacked' log."
> 

> "Only about 5 to 10% of the detects that we get in this industry are from logs." (referring to the logging industrial complex)
> 

> "The tuning is literally our job. We've gotten into this really bad place in security where we expect the tool to automatically do these things for us."
> 

---

*This study guide is formatted for easy import into Notion. Copy and paste the content into a new Notion page to maintain formatting and structure.*