# SOC_Investigation1
Today, you're working as a Tier 1 SOC Analyst. Your job is to investigate a suspicious email reported by an employee.  Your objective is to determine whether this email is malicious, identify potential risks, and recommend what the security team should do next.

> ### 🛡️ CASE SOC-2026-001
>
> **Status:** Open  
> **Investigation:** Under Investigation  
> **Incident:** Suspicious Invoice Email  
> **Alert Source:** Email Security Gateway  
> **Severity:** Medium  
> **Reported By:** Employee (Finance)


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

> ### A Few Terms to Remember
>
> - **IOC (Indicator of Compromise):** A suspicious artifact such as a malicious domain, IP address, or file hash.
> - **URL Reputation:** A service's assessment of whether a web address is known to be safe or malicious.
> - **False Positive:** A legitimate activity that is incorrectly flagged as suspicious.
> - **Phishing:** A deceptive attempt to trick a user into revealing information or interacting with malicious content.

### 5. Your Investigation Tasks
>
> Imagine you're working as a SOC Analyst. Don't rush to declare the email malicious simply because it appears suspicious. Review the evidence and answer the following questions:
>
> 1. **What are the suspicious indicators in this email?**
>    - The sender's email address "accounts[@]finance-payments[.]com", the reply-to email "billing[@]secure-payment[.]net and billing@acme-payments-secure[.]com.
>
> 2. **Is the email definitely malicious?**
>    - The URL hxxps://acme-payments-secure.com/invoice is found to have unknown reputation and could potentially be malicious.
>
> 3. **What would you investigate next?**
>    - Urlscan.io on the this url hxxps://acme-payments-secure.com/invoice and use VirusTotal to check for the file Invoice_1048.zip.
>
> 4. **What is the potential risk?**
>    - If the employee unzips the attachment, there could be a potential data stealer that could steal sensitive company 
>
> 5. **What actions would you recommend?**
>    - Block the sender and flag the email as malicious to prevent further interaction from the email in the future.
>
> 6. **What is your current verdict?**
>   - My final verdict would be to assess that the sender email is malicious and should be blocked to prevent damages in the company.
Preliminary verdict: Confirmed phishing
Please grade my investigation, explain the correct findings, and provide a model incident report.

# 🛡️ SOC-2026-001 — Investigation Review

> [!SUCCESS]
> **Investigation Completed**
>
> **Reviewed By:** Tier 1 SOC Analyst
>
> First, good job completing your first investigation!
>
> I'll review this case as if I were your SOC Team Lead reviewing your investigation notes.
>
> You demonstrated strong security awareness by considering URL reputation, malware analysis, data theft, and containment strategies.
>
> However, one significant issue requires attention:
>
> ⚠️ **You introduced evidence that was not present in the original case.**
>
> This is an important lesson in cybersecurity investigations.
>
> **Always base conclusions on verified evidence, not assumptions.**

---

## 📊 Your Score

> [!NOTE]
> **OVERALL INVESTIGATION SCORE**
>
> ## 68 / 100
>
> ✅ Good First Attempt
>
> *Training assessment only. This is not an industry certification score.*

### Score Breakdown

| Skill | Score |
|---------|---------|
| Identifying Suspicious Indicators | 10/20 |
| Evidence-Based Reasoning | 10/20 |
| Investigation Methodology | 17/20 |
| Understanding Potential Risks | 15/15 |
| Recommended Response | 9/15 |
| Verdict and Confidence | 7/10 |

---

## 📝 Review of Your Answers

<details>
<summary><strong>Question 1 — Suspicious Indicators (10/20)</strong></summary>

### Positive Observations

You identified multiple sender and Reply-To addresses.

Good instinct.

### Issue Identified

Those addresses were not present in the original evidence.

**Actual Sender**

```text
billing@acme-payments-secure.com
```

**Actual URL**

```text
hxxps://acme-payments-secure.com/invoice
```

### Indicators You Should Have Identified

- Unexpected invoice from an unconfirmed sender
- Urgent payment language intended to pressure the recipient
- ZIP attachment (`Invoice_1048.zip`)
- Unknown URL reputation
- Sender domain not verified as a legitimate supplier

### Team Lead Feedback

> Never introduce indicators that haven't been obtained from logs, headers, threat intelligence, or other evidence.
>
> Evidence integrity matters.

</details>

---

<details>
<summary><strong>Question 2 — Is It Definitely Malicious? (10/20)</strong></summary>

You correctly identified the unknown URL reputation.

However:

- Unknown reputation does **not** mean malicious
- Unknown reputation does **not** mean safe

### Additional Investigation Required

- SPF verification
- DKIM verification
- DMARC verification
- Domain reputation analysis
- URL destination validation
- Attachment analysis
- Determine whether the employee opened the attachment

### Recommended Verdict

> ⚠️ Suspicious — Needs Further Investigation

</details>

---

<details>
<summary><strong>Question 3 — What Would You Investigate Next? (17/20)</strong></summary>

### Strong Points

You suggested:

- URLScan.io
- VirusTotal

Both are appropriate tools.

### Additional Investigation Steps

| Tool | Purpose |
|--------|--------|
| VirusTotal | File hash and URL reputation |
| URLScan.io | Website behavior and redirects |
| Email Headers | SPF, DKIM, DMARC verification |
| Sandbox | Observe attachment execution safely |
| SIEM | Search for related activity |

### Team Lead Tip

> Calculate the SHA-256 hash first before checking VirusTotal.
>
> Never upload confidential company attachments to public scanning services without authorization.

</details>

---

<details>
<summary><strong>Question 4 — Potential Risk (15/15)</strong></summary>

✅ Excellent answer.

You mentioned a possible data stealer, which is a realistic concern.

### Possible Payloads

- Executable disguised as an invoice
- Malware downloader
- Malicious shortcut file
- Credential stealer
- Remote Access Trojan (RAT)

### Additional Risks

- Ransomware
- Unauthorized access
- Lateral movement

### Team Lead Tip

Do not assume a payload type until analysis confirms it.

</details>

---

<details>
<summary><strong>Question 5 — Recommended Actions (9/15)</strong></summary>

Blocking the sender is a good containment step, but additional actions are required.

### Expected Tier 1 SOC Response

1. **Quarantine**
   - Remove the email from affected mailboxes
   - Search for additional recipients

2. **Preserve Evidence**
   - Retain email
   - Retain headers
   - Retain attachment
   - Preserve relevant logs

3. **Investigate Exposure**
   - Determine whether the user opened the ZIP
   - Identify any executed files

4. **Threat Hunt**
   - Search endpoints
   - Review SIEM activity
   - Look for related indicators

5. **Block Confirmed Indicators**
   - Domains
   - URLs
   - File hashes

6. **Escalate**
   - Notify Tier 2 SOC
   - Engage Incident Response if compromise is suspected

### Team Lead Tip

> Blocking a sender does not remove malware from a compromised endpoint.

</details>

---

<details>
<summary><strong>Question 6 — Final Verdict (7/10)</strong></summary>

You selected:

❌ **Confirmed Phishing**

Your evidence supported:

⚠️ **Suspicious Email**

### Comparison

| Your Conclusion | Evidence-Based Conclusion |
|----------------|--------------------------|
| Confirmed phishing | Suspicious email |
| Sender is malicious | Sender is unverified |
| URL is malicious | URL reputation unknown |
| Attachment is dangerous | Attachment uninspected |

### Correct Preliminary Verdict

> ⚠️ Suspicious — Needs Further Investigation

This does **not** mean the email is legitimate.

It means there is currently **insufficient evidence** to confirm malicious activity.

### Final Lesson

> Great SOC analysts know when **not** to make a definitive conclusion.
>
> Evidence comes first. Conclusions come second.

</details>

---

## 🎯 Final Team Lead Assessment

> [!TIP]
> **Overall Assessment**
>
> ✅ Strong investigative mindset
>
> ✅ Good understanding of phishing risks
>
> ✅ Appropriate use of security tools
>
> ⚠️ Needs improvement in evidence-based analysis
>
> ⚠️ Avoid assumptions not supported by logs or artifacts
>
> **Recommended Next Step:** Continue practicing investigations while focusing on evidence integrity and confidence-based reporting.


# 📄 Model Investigation Report

> [!IMPORTANT]
> ### SOC INCIDENT REPORT
>
> **Status:** Pending Investigation  
> **Case ID:** SOC-2026-001  
> **Incident Type:** Suspicious Invoice Email  
> **Analyst:** Tier 1 SOC Analyst

---

## 📋 Incident Summary

An employee from the Finance department reported an unexpected invoice email requesting immediate payment.

The email contained:

- A ZIP attachment
- A URL with unknown reputation

---

## 🔍 Initial Indicators

| Indicator | Value |
|------------|---------|
| Sender | `billing@acme-payments-secure.com` |
| Attachment | `Invoice_1048.zip` |
| URL | `hxxps://acme-payments-secure.com/invoice` |
| Received | 6 November 2026, 09:37:21 |
| Reported | 09:42 AM |

---

## ⚠️ Initial Assessment

The email displays several suspicious characteristics:

- Unexpected payment request
- Urgent language designed to pressure the recipient
- Unverified sender domain
- Uninspected ZIP attachment

Based on the available evidence, the email **cannot yet be conclusively classified as malicious.**

---

## 🛠️ Recommended Investigation

1. Inspect email headers and authentication results (SPF, DKIM, DMARC).
2. Calculate the attachment's SHA-256 hash and investigate its reputation.
3. Analyze the URL using approved threat intelligence tools.
4. Determine whether the recipient opened or executed the attachment.
5. Search SIEM and endpoint logs for related activity.

---

## 🚨 Recommended Response

- Quarantine the email.
- Preserve all available evidence.
- Check whether other users received the same message.
- Investigate any interaction with the attachment.
- Escalate suspicious execution activity or signs of compromise.

---

## 📌 Final Disposition

> **Pending Further Investigation**
>
> Assessment based on currently available evidence.

---

# 🎯 Three Things to Remember

> [!TIP]
> These are important habits to develop before entering a real SOC environment.

### 1️⃣ Don't Confuse Suspicion With Confirmation

A suspicious email is **not automatically** a confirmed phishing incident.

Always gather evidence before making a determination.

---

### 2️⃣ Think Beyond the Initial Alert

An email alert is only the starting point.

Ask yourself:

- Did the user click?
- Did a process execute?
- Was there a network connection?
- Did any suspicious activity occur afterward?

---

### 3️⃣ Document What You Know

Document facts, not assumptions.

✅ Good examples:

```text
Hash not yet obtained.
```

```text
User interaction not confirmed.
```

Professional incident documentation clearly distinguishes between known facts and unknown information.

---

# 📚 Next Learning Priorities

| Priority | Topic | Why It Matters |
|-----------|-----------|-----------|
| 1 | Email Headers (SPF, DKIM, DMARC) | Improve phishing investigations |
| 2 | SHA-256 & File Analysis | Learn malware identification techniques |
| 3 | Windows Event Logs | Understand post-execution activity |
| 4 | SIEM Queries | Correlate suspicious events |
| 5 | Incident Response | Learn containment and escalation procedures |

---

# 🏆 Team Lead's Final Assessment

> [!NOTE]
> **Final Score: 68/100**
>
> ✅ Good starting understanding of phishing investigations
>
> ✅ Strong awareness of investigation tools
>
> ✅ Good understanding of potential business impact
>
> ⚠️ Continue improving evidence-based reasoning
>
> ⚠️ Ensure conclusions remain proportional to available evidence
>
> **Recommendation:** Continue performing practical investigations and documenting findings. Real-world investigation practice will accelerate your growth more effectively than focusing solely on theory.
