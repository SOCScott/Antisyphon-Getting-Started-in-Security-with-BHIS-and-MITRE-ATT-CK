# Day 1: Getting Started in Security with BHIS and MITRE ATT&CK

# Day 1: Getting Started in Security with BHIS and MITRE ATT&CK

[https://www.youtube.com/live/cuae43KVtHo](https://www.youtube.com/live/cuae43KVtHo)

## **Introductory Summary**

This cybersecurity training module focuses on practical, effective security controls that actually stop real-world attacks. The instructor, John Strand from Black Hills Information Security (BHIS), emphasizes building foundational skills rather than relying solely on security tools. The session covers 11 critical security controls based on what actually stops penetration testers and attackers in practice, with hands-on labs demonstrating application allow listing and password security. The approach prioritizes practical defense over theoretical knowledge, drawing from BHIS's experience conducting over 650 assessments per year.

---

## Key Takeaways

### 1. **Skills Over Tools Philosophy**

- Building your career around just using tools makes you replaceable by those same tools
- AI will automate repetitive security tasks, but human expertise remains crucial for advanced threats
- Focus on fundamental skills that transfer across different tools and technologies
- Organizations laying off security professionals are typically those who only knew how to use specific tools

### 2. **Practical Security Controls That Actually Work**

- The 11 controls taught in this course are based on what actually stops BHIS's penetration testers
- These controls focus on "triage" - immediate implementations that provide maximum security benefit
- Application allow listing can stop 95% of drive-by downloads and spear phishing attacks with minimal effort
- Password controls should prioritize length over complexity (20+ characters with passphrases)

### 3. **Defense in Depth Strategy**

- Every security technology can and will be bypassed - layered defenses are essential
- Overlapping fields of visibility ensure that if one control fails, others can detect the attack
- Focus on stopping entire categories of attacks rather than individual attack techniques
- The goal is "good enough" security that makes attackers move to easier targets

### 4. **Password Security Reality**

- 8-character passwords can be cracked in hours once an attacker gains access to one system
- Password spraying with seasonal passwords (like "Spring2025") is highly effective against most organizations
- Two-factor authentication doesn't justify weak passwords because many APIs don't support 2FA
- Service accounts are often overlooked and can't use 2FA, making them prime targets

## Complete Study Notes

### Course Philosophy and Industry Context

**AI's Impact on Cybersecurity**

- AI will automate repetitive, mundane security tasks
- Won't replace human expertise for advanced threats like nation-state actors
- Ransomware attacks (repetitive patterns) are good candidates for AI automation
- Advanced persistent threats require human analysis and response
- Industry layoffs are targeting tool-only professionals, not those with fundamental skills

**Real-World Focus vs. Academic Approach**

- Course based on 650+ annual penetration tests by BHIS
- Focuses on what actually stops attackers, not theoretical compliance
- Avoids time-wasting topics like crypto models, security frameworks theory
- Emphasizes practical implementation over perfect security

### The 11 Critical Security Controls

**1. Application Allow Listing**

- Most effective implementation: restrict execution to specific directories only
- Allow execution from: Windows directory, Program Files, Program Files (x86)
- Stops initial access attacks from desktop/temp directories
- Tool: Windows AppLocker (built-in, GPO deployable)
- Creates 3 simple rules vs. trying to catalog every executable

**2. Password Controls**

- Minimum 20 characters (passphrases preferred)
- Length matters more than complexity
- Allow dictionary words to prevent users writing passwords down
- Avoid trading strong passwords for 2FA (APIs often don't support 2FA)
- Service accounts are major vulnerability (no 2FA, often forgotten)

**3. Advanced Endpoint Protection**

- Move beyond signature-based antivirus
- Examples: CrowdStrike, SentinelOne, Huntress, LimaCharlie
- Signature-based detection easily bypassed
- Behavioral analysis and AI-based detection more effective

**4. Logging Strategy**

- Log things that actually help detect attacks
- Don't just "log everything and hope SIEM figures it out"
- Focus on actionable logs for incident response
- Quality over quantity approach

**5. Egress Traffic Analysis**

- Monitor what's leaving your environment
- Many attacks involve data exfiltration or command & control communication
- Network monitoring for suspicious outbound connections

**6. UBA/UEBA (User Behavior Analytics)**

- Detect abnormal user behavior patterns
- Increasingly AI-powered
- Identifies insider threats and compromised accounts
- Baseline normal behavior to spot anomalies

**7. Host Firewalls**

- Stop lateral movement between systems
- Prevent host-to-host communication
- Default deny posture with specific allow rules

**8. Internet Allow Listing**

- Block access to unknown/new domains
- Surprisingly effective with minimal user impact
- Stops communication to newly registered malicious domains

**9. Vulnerability Management**

- "Simple vulnerability management" - focus on critical patches
- Prioritize based on actual exploit risk
- Don't get caught up in low-risk theoretical vulnerabilities

**10. Active Directory Hardening**

- Use tools like PingCastle and BloodHound
- Focus on reducing attack paths
- Secure privileged accounts and admin access

**11. Backup and Recovery**

- Ensure reliable backup systems
- Test restoration procedures regularly
- Critical for ransomware recovery

### Technical Implementation Details

**AppLocker Configuration**

- Enable in Local Security Policy > Application Control Policies
- Configure rule enforcement for executable, installer, script, and package rules
- Create default rules (not auto-generate)
- Start Application Identity service
- Deploy via Group Policy (gpupdate /force)

**Password Attack Methods**

- Password spraying: same password against multiple accounts
- Kerberoasting: extract service account password hashes
- LLMNR/NBT-NS poisoning: intercept authentication attempts
- Cloud-based attacks: rotate IPs through AWS/Azure to avoid blocking

**Bypass Techniques (Awareness)**

- AV evasion through assembly modification
- Living off the Land binaries (LOLBins)
- Encoding/obfuscation tools (Shikata Ga Nai, Unicorn)
- Everything can be bypassed - defense in depth is critical

### Compliance and Standards

**CIS Controls Integration**

- CIS Controls Navigator maps to multiple compliance frameworks
- Acts as "Rosetta Stone" for different standards
- Implementation Groups 1, 2, and 3 provide structured approach
- Cross-references DORA, CMMC, HIPAA, ISO, and others

**MITRE ATT&CK Mapping**

- Course controls address multiple attack techniques simultaneously
- Focus on stopping categories of attacks, not individual techniques
- Application allow listing stops multiple initial access methods
- More efficient than trying to address each technique individually

**Compliance Framework Problems**

- Too many competing standards (XKCD reference: 14 standards → 15 standards)
- Standards often based on outdated assumptions
- NIST Green Book (1985) password requirements still influence modern policies
- PCI only changed from 7 to 14 character minimum in 2023

### Labs and Practical Exercises

**Lab 1: Application Allow Listing**

- Disable AV and firewall for testing
- Create malware with msfvenom
- Mount Windows share from Kali
- Generate reverse shell payload
- Configure AppLocker to block execution
- Demonstrate protection against malware execution

**Lab 2: Password Spraying**

- Generate 200 test users
- Use DomainPasswordSpray tool (by DaftHack)
- Attempt login with "Winter2020" against all users
- Observe successful compromises
- Understand lateral movement possibilities

**Lab 3: Password Cracking**

- Use hashcat against MD5 hashes
- Crack Windows NT password hashes
- Demonstrate speed of modern password cracking
- Understand why longer passwords are essential

### Tools and Resources

**Free Training Resources**

- SOC Core Skills class available on YouTube
- Attack Tactics webcast series
- Back Doors and Breaches card game
- BHIS GitHub repository with lab files

**Cloud Lab Environment**

- MetaCTF provides browser-based VMs
- 16 hours of lab time provided
- Kali Linux and Windows VMs available
- Destroy and restart labs to conserve credits

**Password Management**

- Use password managers (avoid LastPass after breaches)
- Examples: Secret Server, 1Password, Bitwarden
- Enable 2FA on password manager account
- Generate unique passwords for each service

---

## **Quick Quiz**

### **Question 1**

What is the primary reason John Strand recommends against focusing solely on security tools rather than foundational skills?

**Answer:** Security professionals who only know how to use tools are at risk of being replaced by those tools/AI. Recent industry layoffs have primarily affected people who focused on tool operation (like CrowdStrike, Sentinel One) rather than developing core Windows, Linux, and networking skills. Building fundamental knowledge makes you irreplaceable.

### **Question 2**

According to the training, what three directories should be included in a basic AppLocker allow listing policy?

**Answer:**

1. Windows directory
2. Program Files directory
3. Built-in Administrator accounts
These three default rules allow systems to run efficiently while blocking malware execution from common attack vectors like desktop downloads or temporary internet directories.

### **Question 3**

Why does the instructor argue that password length is more important than complexity, and what minimum length does he recommend?

**Answer:** Password length is the only factor that truly matters for security because longer passwords exponentially increase cracking time. The instructor recommends a minimum of 20 characters. Complex but short passwords (8-10 characters) can be cracked in hours with modern GPU-based attacks, while longer passphrases using dictionary words are both more secure and user-friendly.

### **Question 4**

What is Kerberoasting and why was it initially rejected by major security conferences?

**Answer:** Kerberoasting is an attack where any user account can request ticket-granting tickets for service accounts, which contain the service account's password hash. The attacker can then crack these hashes offline. It was initially rejected by Black Hat and DEF CON because it seemed too simple or unbelievable, but it fundamentally changed attack methodologies in Windows environments. Tim Medin, who discovered this technique, was eventually accepted at DerbyCon where it became recognized as a critical security issue.

---

## **Notable Quotes**

> "If you build your entire life around using a tool, that tool will find a way to replace you."
> 

> "We're getting our asses absolutely kicked in computer security at the moment... it's not like we can just have AI magically come in and solve our computer security issues because the issues that we're seeing are very much systemic across the board.”
> 

> "Everything can and will be bypassed. Every single technology that you use in your organization can and will be bypassed.”
> 

> "The only thing that matters [for password security] is length. It's the absolute only thing.”
> 

> "We're not trying to get to 100% security, we're trying to get us to good enough." (On practical security implementation)
> 

> "Once I get your session identifier, I am you at that point. I don't even need to know what your password is." (On session hijacking)
>