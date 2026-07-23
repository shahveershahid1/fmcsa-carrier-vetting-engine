# 🚛 FMCSA Carrier Vetting & Risk Evaluation Engine

An automated carrier compliance and risk evaluation engine built on **n8n**. This workflow streamlines carrier onboarding for freight brokerages and 3PLs by automatically validating USDOT operating authority, evaluating safety metrics, and enforcing automated pass/fail routing to prevent double-brokering, cargo theft, and compliance liabilities.

---

## 📌 Problem Statement

Freight brokers and 3PLs spend **10–15 minutes per load** manually cross-referencing carrier details on the FMCSA portal. Manual verification creates major operational bottlenecks and leaves brokerages vulnerable to:
* **Double-brokering and cargo fraud** by unverified bad actors.
* **Non-compliant hauling** using revoked or inactive operating authorities.
* **Safety risks** from carriers with high Out-of-Service (OOS) driver rates.

---

## 💡 Solution Overview

This workflow automates the entire carrier vetting process into a **2-second automated pipeline**:
1. Captures USDOT inputs via a lightweight web portal (Form Trigger).
2. Queries/evaluates carrier safety metrics (Operating status, OOS rates, authority).
3. Evaluates custom compliance rules programmatically inside a JavaScript execution engine.
4. Automatically routes approved carriers to an audit log while immediately flagging high-risk carriers across Slack and email channels.

---

## ⚙️ Key Features

* **Real-Time Authority Verification:** Checks if an MC/DOT operating authority is active (`statusCode: "A"`) and authorized (`allowedToOperate: "Y"`).
* **Automated Safety Thresholds:** Evaluates driver Out-of-Service (OOS) percentages and flags carriers exceeding acceptable risk thresholds (> 25%).
* **Multi-Channel Escalation:** 
  * **Approved:** Logs carrier details in Google Sheets and posts a green light alert in Slack.
  * **Flagged / Denied:** Sends an immediate red alert to a Slack compliance channel and triggers an escalation email to halt booking.
* **Audit Trail:** Maintains structured, timestamped logs for compliance audits.

---

## 🛠 Tech Stack

| Component | Technology / Node |
| :--- | :--- |
| **Orchestration** | n8n |
| **Trigger** | n8n Form Trigger |
| **Logic & Business Rules** | JavaScript (n8n Code Nodes) |
| **Routing** | IF Node (Conditional Branching) |
| **Database / Logging** | Google Sheets API |
| **Alerts & Notifications** | Slack API & Gmail API |

---

## 📦 How to Run

1. **Import the Workflow:**
   * Download `workflow.json` from this repository.
   * In n8n, go to **Settings** ➔ **Import from File** and select `workflow.json`.

2. **Set Up Credentials:**
   * Connect your **Google Sheets**, **Slack**, and **Gmail** accounts in n8n.

3. **Execute & Test:**
   * Publish the workflow.
   * Open the Form URL, enter a test USDOT number (e.g., `221515`), and submit.

<img width="1680" height="929" alt="Screenshot 2026-07-23 at 9 57 32 AM" src="https://github.com/user-attachments/assets/31cf60d4-840f-4331-a2f0-248e1e117eac" />
