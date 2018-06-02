---
layout: kab
group: rs
title: Classification Sample
---

The data classification system is based on the principle of least privilege. This principle stipulates that accounts have the least amount of privilege required to perform their business processes, or that information is not disclosed or assessible to any person who does not have a legitimate and demonstrable business need to receive the information. This principle in combination with the measures detailed in the matrix will protect the Company and its customers’ information from unauthorized disclosure, use, modification, and deletion. 
### Data Classification Matrix

||Public|Proprietary|Confidential|
|---|---|---|---|
|Information Classification Guideline|Information is not confidential and can be made public without any implications for Company. Loss of availability due to system downtime is an acceptable risk. Integrity is important but not vital.|Unauthorized access could influence the Company's operational effectiveness, cause meaningful financial loss, provide a significant gain to a competitor, or cause a substantial reduction in customer confidence.|Information which by regulation or contractual obligation must be secured from unauthorized exposure or only exposed upon obtaining written authorization.|
|<br/><br/>|<br/><br/>|<br/><br/>|<br/><br/>|
|Classification of Common Data Elements<br/><br/><br/><br/>|-- Marketing material<br>-- Public filings<br>-- Public web site material|-- Company goals and objectives<br>-- Macro financial data such as what is reported on our dashboard<br>--  Organizational charts<br>|-- Protected individually identifying information<br>-- data covered by PCI (bank account numbers, credit card numbers, etc)<br>-- Third party data elements protected by contract terms|
|<br/><br/>|<br/><br/>|<br/><br/>|<br/><br/>|
|Access and Authentication Controls<br/><br/><br/><br/>|None|-- Information is restricted to management and authorized staff based on  supervisor approval.<br>-- Information is protected from external access.* |Information is restricted on a need-to-know basis<br>-- Role based access control<br>-- Systems presenting data must be password protected.<br>–- Formal approval by supervisor* |
|===|===|===|===|
|Security Controls<br/><br/><br/><br/>|None|-- Encryption at rest<br>-- Systems protected from direct access by external systems via firewall* |-- End-to-end encryption<br>-- Systems protected from direct access by external systems via a firewall in the DMZ* |
|===|===|===|===|
|Transmission Controls<br/><br/><br/><br/>|None|Data at this level that is transmitted to external parties must be encrypted* |Data at this level must be encrypted (internal network or outside the Company network)* |
|===|===|===|===|
|Storage<br/><br/><br/><br/>|-- Plain text<br>-- Backup is recommended|-- Encryption at rest at disk/media level<br>-- Backup is required* |-- Encryption at rest at disk/media and file level<br>Encrypted backup at off-site storage is required* <br>-- Physical media must be reformatted before re-use* |

\* Applies unless there is an approved exception or a waiver has been issued.

<br/>
<br/>
