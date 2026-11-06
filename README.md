# SOC_Investigation1
Today, you're working as a Tier 1 SOC Analyst. Your job is to investigate a suspicious email reported by an employee.  Your objective is to determine whether this email is malicious, identify potential risks, and recommend what the security team should do next.

> ### 🛡️ CASE SOC-2026-001
>
> |Status:| Open  
> |Investigation:| Under Investigation  
> |Incident:| Suspicious Invoice Email  
> |Alert Source:| Email Security Gateway  
> |Severity:| Medium  
> |Reported By:| Employee (Finance)


### 1. Incident scenario
At 09:42 AM, an employee from the Finance department reports receiving an unexpected email claiming to contain an outstanding invoice.

The employee says:
"I wasn't expecting an invoice from this company. The email says payment is overdue and asks me to download the attached document."

The employee has not confirmed whether they opened the attachment.

Your SOC team has assigned this alert to you.

### 2. Email Details
>
> | Field | Value |
> |--------|--------|
> | Subject | Invoice Payment Reminder - Due Today |
> | Sender | accounts@finance-payments.com |
> | Recipient | finance.employee@company.com |
> | Date Received | 2026-01-15 09:42 UTC |
> | Reply-To | billing@secure-payment.net |
> | Attachment | Invoice_2026_001.pdf |
> | Message Type | External Email |

### 3. Email security gateway logs
The following are fictional training logs created for this investigation.

2026-11-06 09:37:21
EVENT: INBOUND_EMAIL_RECEIVED
SENDER: billing@acme-payments-secure.com
RECIPIENT: employee@company.com

2026-11-06 09:37:22
EVENT: ATTACHMENT_SCANNED
FILENAME: Invoice_1048.zip
FILETYPE: application/zip
SIZE: 245 KB

2026-11-06 09:37:23
EVENT: URL_REPUTATION_CHECK
URL: hxxps://acme-payments-secure.com/invoice
RESULT: UNKNOWN

2026-11-06 09:37:24
EVENT: SPAM_FILTER
RESULT: DELIVERED
REASON: No known malicious signature detected

### 4. Additional indicators
Indicator	Value
Sender domain	acme-payments-secure.com
Attachment	ZIP archive
URL reputation	Unknown
Email urgency	High
Expected invoice	Not confirmed

### A few terms to remember:
> |IOC:| Indicator of Compromise, such as a suspicious domain or file hash.
> |URL reputation:| A service's assessment of whether a web address is known to be malicious.
> |False positive:| A legitimate activity incorrectly flagged as suspicious.
> |Phishing:| A deceptive attempt to trick someone into revealing information or executing malicious content.
