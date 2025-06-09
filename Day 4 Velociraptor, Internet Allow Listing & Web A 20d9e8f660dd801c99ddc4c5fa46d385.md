# Day 4: Velociraptor, Internet Allow Listing & Web App Security

## Introduction Summary

Day 4 completes the security fundamentals course by covering advanced incident response capabilities with Velociraptor, internet allow listing strategies, effective vulnerability management approaches, and web application security testing. The session emphasizes practical tools that provide immediate security value: Velociraptor for enterprise-scale incident response, internet allow listing to block unknown domains, vulnerability management focused on systemic fixes rather than individual IP addresses, and automated web application scanning. The instructor concludes with reflections on the pay-what-you-can training philosophy and the importance of breaking down financial barriers to cybersecurity education.

## Key Takeaways

### 1. **Enterprise Incident Response with Free Tools**

- Velociraptor (free, open-source) can outperform expensive commercial EDR solutions
- 58MB executable handles both client and server functionality for massive scalability
- Real-world example: BHIS used Velociraptor when commercial EDR maxed out at 10,000 hosts
- Hunt capabilities across thousands of endpoints provide superior visibility than many paid tools

### 2. **Internet Allow Listing is Surprisingly Effective**

- Most users visit fewer than 25 legitimate websites regularly
- Blocking "uncategorized" domains stops attacks using newly registered domains
- Attackers often register domains, use them briefly, then get refunds within 7 days
- Ad blocking prevents sophisticated malvertising attacks including nation-state zero-click exploits

### 3. **Vulnerability Management Strategy Revolution**

- Group vulnerabilities by plugin/CVE ID, not by IP address (1000 IPs × 25 vulns ≠ 25,000 problems)
- One vulnerability on 400 systems = one fix deployed 400 times, not 400 separate issues
- Focus on "low" and "informational" findings - these often provide actual access
- Configuration vulnerabilities (Active Directory) are as critical as missing patches

### 4. **Automated Security Testing Democratizes Protection**

- 90% of web application vulnerabilities are easily found by free automated tools
- Zed Attack Proxy (ZAP) provides capabilities rivaling $20,000+ commercial scanners
- Security should be integrated throughout development, not bolted on at the end
- Testing before hiring penetration testers focuses expert time on complex business logic issues

## Complete Study Notes

### Velociraptor for Enterprise Incident Response

**Velociraptor Architecture and Deployment**

- Single 58MB executable functions as both client and server
- Server generates configuration files that get pushed to endpoints
- Similar deployment model to Lima Charlie, Elastic, and other enterprise EDR solutions
- Self-signed SSL certificates acceptable for internal deployments
- Web-based management interface with unique client GUIDs for each endpoint

**Configuration and Setup Process**

- Server configuration: `velociraptor config generate` with mostly default settings
- Client enrollment: MSI deployment pushes files to Program Files directories
- Authentication: Create GUI users with username/password for web interface
- Service deployment: Clients connect back to server automatically after configuration
- Group Policy deployment: Shared server location with executable and config files

**Hunt Capabilities and Artifacts**

- Targeted hunts across multiple systems simultaneously
- Artifact selection: Process hierarchy (PS3), file system analysis, registry examination
- Hunt scheduling and management through web interface
- CSV export of results for analysis and reporting
- Command execution against individual or multiple endpoints remotely

**Commercial EDR Limitations - Real-World Example**

- CyFort maxed out at 10,000 hosts for environment-wide queries
- Commercial limitations forced BHIS to deploy free Velociraptor for large customer
- Many commercial EDRs lack deep forensic capabilities during active incidents
- SentinelOne historical limitations in file system and registry access during IR
- Velociraptor filled gaps that expensive commercial solutions couldn't address

**Incident Response Applications**

- Remote forensic data collection without permanent agent installation
- Process hierarchy analysis for attack pattern identification
- File system and registry examination across entire enterprise
- Timeline analysis and artifact correlation
- Threat hunting across thousands of endpoints simultaneously

### Internet Allow Listing Strategy

**User Browsing Behavior Analysis**

- Average user visits fewer than 25 legitimate websites regularly
- Most traffic concentrated on major platforms: Facebook, LinkedIn, news sites
- Business vs. personal usage distinction less important than security impact
- Social engineering relies on users clicking every link they encounter
- Legitimate business needs can be accommodated within allow listing framework

**Uncategorized Domain Blocking**

- Critical to block domains never seen by major security vendors
- Microsoft, Fortinet, Cisco categorization databases provide baseline
- New domains default to "uncategorized" status until reviewed
- Attackers exploit uncategorized status for short-term domain abuse
- Allow listing prevents access to newly registered malicious domains

**Attacker Domain Registration Patterns**

- Domain registrars offer 7-day money-back guarantee periods
- Attackers register domains, conduct attacks, then request refunds
- Cycle through multiple disposable domains for campaign duration
- DNS providers see constant flux of uncategorized domains
- Traditional deny listing cannot keep pace with domain rotation

**Malvertising and Nation-State Threats**

- NSO Group demonstrates zero-click malware delivery through advertising
- Geographic targeting: Draw squares around buildings for precise ad delivery
- Demographic targeting: Age, gender, device type for surgical precision
- Nation-state actors use different methodologies than ransomware criminals
- Ad blocking becomes critical defense against sophisticated targeting

**Implementation Considerations**

- Category-based allow listing more practical than individual site management
- User request systems for new legitimate sites
- DNS over HTTPS can bypass domain-based filtering
- VPN usage considerations for advanced users
- Balance between security and usability for business operations

### Vulnerability Management Revolution

**The IP Address Grouping Problem**

- Traditional approach: Group vulnerabilities by individual IP address
- Result: 1,000 IPs × 25 vulnerabilities = 25,000 overwhelming individual issues
- Reality: Many vulnerabilities are identical across multiple systems
- Correct approach: Group by vulnerability type/plugin ID, not IP address
- Mental shift: One vulnerability affecting 400 systems = one systematic fix

**Systematic Remediation Approach**

- Identify vulnerability types that repeat across multiple systems
- Example: TLS/SSL vulnerabilities on 400 web servers = one configuration change
- Automation tools: Ansible, Puppet, Chef, SCCM for mass deployment
- Group Policy for Windows-specific configuration vulnerabilities
- Focus effort on creating systematic fixes rather than individual patches

**The "Low and Informational" Vulnerability Trap**

- Organizations typically fix only "Critical" and "High" severity findings
- "Low" and "Informational" vulnerabilities accumulate into "snowball of poop"
- Real-world penetration testing often succeeds through low-severity findings
- Example: Telnet services rated "Low" but provide direct administrative access
- BHIS finds exploitable Telnet approximately once per quarter in enterprise environments

**Active Directory Configuration Vulnerabilities**

- PingCastle analysis reveals systemic configuration weaknesses
- Empty passwords on service accounts
- Password never expires settings on user accounts
- "Everyone" permissions meaning anonymous access (not authenticated users)
- Stale accounts with ancient passwords (2014 last logon examples)
- Configuration vulnerabilities often more critical than missing patches

**BHIS Vulnerability Management Success Story**

- Over 1 million live IP addresses assessed by 2 analysts in 3 weeks
- Competing consulting firm: 5 consultants for 3 months at $400,000 cost
- BHIS found hundreds of exploitable systems missed by expensive competitor
- Success attributed to vulnerability grouping methodology, not just tools
- Demonstrates power of systematic approach over traditional IP-based analysis

### Web Application Security Testing

**The Training and Tool Cost Problem**

- Traditional web application security training costs $10,000+ per person
- Commercial web application testing tools cost $20,000+ annually
- High costs create executive "YOLO" attitudes toward application security
- Industry artificially inflates complexity to justify expensive solutions
- Free and open-source tools provide comparable capabilities at zero cost

**Software Development Lifecycle Integration**

- Security traditionally "bolted on" at the end of development cycles
- Common scenario: "We go live in 3 weeks, need clean bill of health"
- BHIS refuses pure compliance checkbox engagements
- Continuous testing throughout development cycle prevents last-minute surprises
- Applies to both custom development and commercial off-the-shelf software

**The 90/10 Rule for Web Application Vulnerabilities**

- 90% of vulnerabilities are easily identified and remediated
- 10% require 90% of the expert effort (business logic, complex authorization)
- Automated tools excel at finding the easy 90%: SQL injection, XSS, misconfigurations
- Manual testing required for complex issues: business logic errors, permission flaws
- Cost-effective strategy: Automate the easy stuff, focus experts on hard problems

**Tool Recommendations and Capabilities**

- **Burp Suite Pro**: Most heavily used in industry (~$500, excellent value)
- **Zed Attack Proxy (ZAP)**: Free alternative with comparable automated scanning
- **W3AF**: Another automated scanner option
- **Nickto**: BHIS-developed tool for default content vulnerabilities
- **Damn Small Vulnerable Web App**: Training environment for testing tools

**ZAP Automated Scanning Process**

- Spider crawls website to discover all URLs and parameters
- Automated attack phase launches thousands of vulnerability tests
- Request/response analysis shows exact attack strings and results
- Vulnerability categorization with severity ratings and remediation guidance
- Integration with OWASP references for detailed vulnerability research

**Getting Caught Testing - The Detection Imperative**

- Vulnerability testing should trigger security monitoring systems
- Web application attacks generate enormous amounts of log data
- Most web application attacks are not stealthy - intentionally noisy
- Testing validates both vulnerabilities AND detection capabilities
- Framework shift: "Can we be hacked?" → "What can we detect?"

### Professional Development and Industry Philosophy

**The Certification Alternative**

- Anti-Siphon Certification (AC) replaces traditional multiple-choice tests
- Multiple choice component + practical cyber range challenges + written reports
- Public profile system allows employers to evaluate actual work quality
- Bidirectional validation: Candidates prove skills, employers verify capabilities
- Addresses industry frustration with expensive, ineffective certification programs

**The Pay-What-You-Can Philosophy**

- Traditional scholarships are "photo ops" that don't change systemic barriers
- Financial barriers affect all demographics: rural white, urban minorities, indigenous peoples
- "Burn the gates down" for everyone rather than selective scholarship programs
- People who can't pay monetarily pay with their most valuable asset: time
- Recognition that economic circumstances don't reflect personal value or potential

**Skills Gap vs. Job Market Reality**

- Industry layoffs affect tool-users, not fundamental skills practitioners
- College graduates lack practical command-line and networking knowledge
- Hiring managers report inability to find qualified candidates despite unemployment
- Need for upcoming "Why You're Not Getting Hired" webcast addressing skills gaps
- Emphasis on fundamentals that transfer across tools and technologies

**Community Building and Knowledge Sharing**

- Over 250 confirmed job placements through BHIS programs (bell ringing tradition)
- Emphasis on giving back to community rather than hoarding knowledge
- Social media amplification requests to reach more people needing training
- Recognition of both paying students (generosity) and non-paying students (time investment)
- Long-term vision of industry transformation through accessible education

## Quiz Questions

1. **Question**: Describe the real-world scenario where Velociraptor outperformed a commercial EDR solution, and explain why this demonstrates the importance of capability over cost.
    - **Answer**: During a large incident response engagement, BHIS needed to query across an entire enterprise environment to identify specific processes on all systems. The customer's commercial EDR solution (CyFort) had a hard limit of 10,000 hosts for environment-wide queries. When the customer had more than 10,000 systems, the commercial tool simply couldn't generate the needed report. BHIS had to deploy the free, open-source Velociraptor tool across all systems to get the comprehensive data required for the investigation. This demonstrates that expensive commercial solutions can have arbitrary limitations that free tools don't have, and that capability and flexibility matter more than price. The 58MB Velociraptor executable provided better scalability than a tool costing thousands of dollars annually.

2. **Question**: Explain the vulnerability management "IP address grouping problem" and how changing the approach can dramatically reduce remediation effort.
    - **Answer**: The traditional approach groups vulnerabilities by IP address, creating an overwhelming number of seemingly individual issues. For example: 1,000 IP addresses × 25 vulnerabilities each = 25,000 separate problems to fix. This approach is fundamentally wrong because many vulnerabilities are identical across multiple systems. The correct approach groups vulnerabilities by plugin ID or CVE number. Using the same example: if 400 web servers all have the same TLS/SSL vulnerability, that's not 400 separate problems - it's one vulnerability affecting 400 systems, requiring one systematic fix deployed 400 times. This mental shift allows organizations to use automation tools (Ansible, Puppet, Chef, Group Policy) to remediate vulnerabilities at scale. BHIS demonstrated this by having 2 analysts address all vulnerabilities across over 1 million live IP addresses in 3 weeks, while a competing firm needed 5 consultants for 3 months on the same project.

3. **Question**: Why is blocking "uncategorized" domains so effective against modern attack campaigns, and how do attackers exploit domain registration systems?
    - **Answer**: Blocking uncategorized domains is effective because attackers frequently register new domains that haven't been seen or categorized by major security vendors (Microsoft, Fortinet, Cisco). Many domain registrars offer 7-day money-back guarantees, which attackers exploit by registering domains, conducting attacks, then requesting full refunds before the deadline. This allows them to cycle through multiple "disposable" domains during a campaign without accumulating costs. Since these domains are newly registered and unknown to security vendors, they appear as "uncategorized" in filtering systems. Most legitimate users visit fewer than 25 websites regularly, so blocking uncategorized domains has minimal impact on business operations while preventing access to newly registered attack infrastructure. This approach is more effective than traditional deny listing because attackers can register new domains faster than deny lists can be updated.

4. **Question**: What does the instructor mean by the "90/10 rule" for web application vulnerabilities, and how should organizations structure their security testing strategy around this principle?
    - **Answer**: The 90/10 rule states that 90% of web application vulnerabilities are easily identified and fixed, while 10% of vulnerabilities require 90% of the expert effort to find and remediate. The easy 90% includes common issues like SQL injection, cross-site scripting, and misconfigurations that automated tools can reliably detect. The difficult 10% includes business logic errors, complex authorization flaws, and application-specific issues that require manual testing and deep understanding of the application's intended functionality. Organizations should structure their testing strategy by using free automated tools (like Zed Attack Proxy) to find and fix the easy 90% of issues before engaging expensive penetration testing firms. This allows expert testers to focus their time and expertise on the complex 10% that actually requires human intelligence and creativity, making security testing both more effective and cost-efficient.

## Notable Quotes

> "The internet is big. Really big. You just wouldn't believe how vastly mind-boggingly huge it actually is. And most of it is worthless and evil."
> 

> "In computer security we have a problem where people are trying to say that certain things are so incredibly difficult that the only way you can solve that problem is by buying an expensive product."
> 

> "Instead of looking at 25,000 individual vulnerabilities, you're actually looking at a few hundred that repeat multiple times on multiple systems."
> 

> "Security is hard. Not really. I think that information security, one of the main reasons that people think security is hard is because the industry is trying to make it hard."
> 

> "Most web application attacks are not stealthy. They're an attacker running lots and lots and lots of different checks to try to gain access to the server itself."
> 

> "90% of the issues are easy to identify, easy to address and easy to take care of. And 10% take 90% of the effort."
> 

---
