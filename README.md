# FMCSA Carrier Vetting & Risk Evaluation Engine (n8n)

An automated carrier compliance and risk evaluation workflow built with **n8n**. This solution streamlines carrier onboarding for freight brokerages and 3PLs by automatically validating USDOT operating authority, evaluating safety metrics, and enforcing automated pass/fail routing to prevent double-brokering and cargo fraud.

---

## 📸 Workflow Architecture

```text
 [Form Submission Trigger] (Dispatcher inputs USDOT Number)
            │
            ▼
 [FMCSA SAFER API Engine] (Queries Carrier Safety & Authority Data)
            │
            ▼
 [Risk Evaluation Engine] (JavaScript Code Node: Authority & OOS Checks)
            │
            ├── (Status == APPROVED) ──> [Google Sheets] (Log Audit Trail)
            │                                 │
            │                                 ▼
            │                          [Slack Channel] (Green Approval Alert)
            │
            └── (Status == DENIED/FLAGGED) ──> [Slack Channel] (Red Risk Alert)
                                                      │
                                                      ▼
                                               [Gmail] (Compliance Team Escalation)
🚀 Key Features & Operational Business Impact
Real-Time Authority Verification: Instantly checks if an MC/DOT operating authority is active (statusCode: "A") and permitted to operate (allowedToOperate: "Y").

Automated Safety Score Thresholds: Evaluates the carrier's Driver Out-of-Service (OOS) Rate. Automatically flags any carrier exceeding the safety risk threshold (e.g., > 25%).

Multi-Branch Action Routing:

Approved Carriers: Appends structured audit data directly into Google Sheets and notifies the dispatch team on Slack in seconds.

High-Risk Carriers: Sends an immediate red-flag alert to a dedicated Slack compliance channel and issues an urgent Gmail escalation to halt load booking.

Fraud Mitigation: Protects freight brokerages from cargo theft, double-brokering, and non-compliant haulers without requiring manual FMCSA portal lookups.

🛠 Tech Stack & Nodes Used
n8n: Workflow orchestration engine.

Form Trigger: Web portal interface for dispatchers.

JavaScript (Code Nodes): Payload transformation, business rule evaluation, and conditional scoring logic.

IF Node: Branching execution paths based on evaluated risk status.

Google Sheets API: Persistent record keeping and compliance logging.

Slack API & Gmail API: Multi-channel alerting and stakeholder notifications.

⚙️ Installation & Setup
Import Workflow:

Download the workflow.json file from this repository.

Open your n8n canvas, click Settings -> Import from File, and upload workflow.json.

Configure Credentials:

Authenticate your Google Sheets node.

Authenticate your Slack and Gmail nodes (or replace with your preferred communication tools).

Activate & Test:

Publish the workflow.

Open the generated Form URL, enter a test USDOT number (e.g., 221515), and execute.

<img width="1680" height="929" alt="Screenshot 2026-07-23 at 9 57 32 AM" src="https://github.com/user-attachments/assets/dda70cac-6da5-4f0f-9c7c-a911082d35af" />

