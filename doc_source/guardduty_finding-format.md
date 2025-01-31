# GuardDuty finding format<a name="guardduty_finding-format"></a>

When GuardDuty detects suspicious or unexpected behavior in your AWS environment, it generates a finding\. A finding is a notification that contains the details about a potential security issue that GuardDuty discovers\. The [finding details](guardduty_findings.md#guardduty_working-with-findings) include information about what happened, which AWS resources were involved in the suspicious activity, when this activity took place, and other information\.

One of the most useful pieces of information in the finding details is a **finding type**\. The purpose of the finding type is to provide a concise yet readable description of the potential security issue\. For example, the GuardDuty *Recon:EC2/PortProbeUnprotectedPort* finding type quickly informs you that somewhere in your AWS environment, an EC2 instance has an unprotected port that a potential attacker is probing\.

GuardDuty uses the following format for naming the various types of findings that it generates:

**ThreatPurpose:ResourceTypeAffected/ThreatFamilyName\.DetectionMechanism\!Artifact**

Each part of this format represents an aspect of a finding type\. These aspects have the following explanations:
+ **ThreatPurpose** \- describes the primary purpose of a threat, an attack type or a stage of a potential attack\. See the following section for a complete list of GuardDuty threat purposes\.
+ **ResourceTypeAffected** \- describes which AWS resource type is identified in this finding as the potential target of an adversary\. Currently GuardDuty can generate findings for EC2, IAM, and S3 resources\.
+ **ThreatFamilyName** \- describes the overall threat or potential malicious activity that GuardDuty is detecting\. For example, a value of **NetworkPortUnusual** indicates that an EC2 instance identified in the GuardDuty finding has no prior history of communications on a particular remote port that also is identified in the finding\.
+ **DetectionMechanism** \- describes the method in which GuardDuty detected the finding\. This can be used to indicate a variation on a common finding type or a finding that GuardDuty used a specific mechanism to detect\. For example, **Backdoor:EC2/DenialOfService\.Tcp** indicates denial of service \(DoS\) was detected over TCP\. The UDP variant is **Backdoor:EC2/DenialOfService\.Udp**\.

  A value of **\.Custom** indicates that GuardDuty detected the finding based on your custom threat lists, while **\.Reputation** indicates that GuardDuty detected the finding using a domain reputation score model\.
+ **Artifact** \- describes a specific resource that is owned by a tool that is used in the malicious activity\. For example, **DNS** in the finding type *CryptoCurrency:EC2/BitcoinTool\.B\!DNS* indicates that an EC2 instance is communicating with a known Bitcoin\-related domain\.

## Threat Purposes<a name="guardduty_threat_purposes"></a>

In GuardDuty a *threat purpose* describes the primary purpose of a threat, an attack type, or a stage of a potential attack\. For example, some threat purposes, such as **Backdoor**, indicate a type of attack\. However some threat purposes, such as **Impact** align with [MITRE ATT&CK tactics](https://attack.mitre.org/tactics/TA0010/)\. The MITRE ATT&CK tactics indicate different phases in an adversary's attack cycle\. In the current release of GuardDuty, ThreatPurpose can have the following values:

**Backdoor**  
This value indicates that an adversary has compromised an AWS resource and altered the resource so that it is capable of contacting its home command and control \(C&C\) server to receive further instructions for malicious activity\.

**Behavior**  
This value indicates that GuardDuty has detected activity or activity patterns that are different from the established baseline for the AWS resources involved\.

**CredentialAccess**  
This value indicates that GuardDuty has detected activity patterns that an adversary may use to steal credentials, such as account IDs or passwords, from your environment\. This threat purpose is based on [MITRE ATT&CK tactics](https://attack.mitre.org/matrices/enterprise/cloud/aws/)

**Cryptocurrency**  
This value indicates that GuardDuty has detected that an AWS resource in your environment is hosting software that is associated with cryptocurrencies \(for example, Bitcoin\)\.

**DefenseEvasion**  
This value indicates that GuardDuty has detected activity or activity patterns that an adversary may use to avoid detection while infiltrating your environment\. This threat purpose is based on [MITRE ATT&CK tactics](https://attack.mitre.org/matrices/enterprise/cloud/aws/)

**Discovery**  
This value indicates that GuardDuty has detected activity or activity patterns that an adversary may use to expand their knowledge of your systems and internal networks\. This threat purpose is based on [MITRE ATT&CK tactics](https://attack.mitre.org/matrices/enterprise/cloud/aws/)\.

**Exfiltration**  
This value indicates that GuardDuty has detected activity or activity patterns that an adversary may use when attempting to steal data from your network\. This threat purpose is based on [MITRE ATT&CK tactics](https://attack.mitre.org/tactics/TA0010/)\.

**Impact**  
This value indicates that GuardDuty has detected activity or activity patterns that suggest that an adversary is attempting to manipulate, interrupt, or destroy your systems and data\. This threat purpose is based on [MITRE ATT&CK tactics](https://attack.mitre.org/matrices/enterprise/cloud/aws/)

**InitialAccess**  
This threat purpose is based on [MITRE ATT&CK tactics](https://attack.mitre.org/matrices/enterprise/cloud/aws/)

**Pentest**  
**** Sometimes owners of AWS resources or their authorized representatives intentionally run tests against AWS applications to find vulnerabilities, such as open security groups or access keys that are overly\-permissive\. These pen tests are done in an attempt to identify and lock down vulnerable resources before they are discovered by adversaries\. However, some of the tools used by authorized pen testers are freely available and therefore can be used by unauthorized users or adversaries to run probing tests\. Although GuardDuty can't identify the true purpose behind such activity, the **Pentest** value indicates that GuardDuty is detecting such activity, that it is similar to the activity generated by known pen testing tools, and that it could indicate malicious probing of your network\.

**Persistence**  
This value indicates that GuardDuty has detected activity or activity patterns that an adversary may use to try and maintain access to your systems even if their initial access route is cut off\. For example, this could include creating a new IAM user after gaining access through an existing user's compromised credentials\. When the existing user's credentials are deleted, the adversary will retain access on the new user that was not detected as part of the original event\. This threat purpose is based on [MITRE ATT&CK tactics](https://attack.mitre.org/matrices/enterprise/cloud/aws/)\.

**Policy**  
This value indicates that your AWS account is exhibiting behavior that goes against recommended security best practices\. 

**PrivilegeEscalation**  
This value informs you that the involved principal within your AWS environment is exhibiting behavior that an adversary may use to gain higher\-level permissions to your network\. This threat purpose is based on [MITRE ATT&CK tactics](https://attack.mitre.org/matrices/enterprise/cloud/aws/)\.

**Recon**  
This value indicates that GuardDuty has detected activity or activity patterns that an adversary may use when preforming reconnaissance of your network to determine how they can broaden their access or utilize your resources\. For example, this activity can include scoping out vulnerabilities in your AWS environment by probing ports, listing users, database tables, and so on\.

**Stealth**  
This value indicates that an adversary is actively trying to hide their actions\. For example, they might use an anonymizing proxy server, making it extremely difficult to gauge the true nature of the activity\.

**Trojan**  
This value indicates that an attack is using Trojan programs that silently carry out malicious activity\. Sometimes this software takes on an appearance of a legitimate program\. Sometimes users accidentally run this software\. Other times this software might run automatically by exploiting a vulnerability\. 

**UnauthorizedAccess**  
This value indicates that GuardDuty is detecting suspicious activity or a suspicious activity pattern by an unauthorized individual\.