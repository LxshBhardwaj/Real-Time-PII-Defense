🚨 Problem Statement
Flixkart, one of the largest online retail platforms, underwent a security audit to assess customer data protection. While the core repositories were well-guarded, auditors discovered that PII (Personally Identifiable Information) was leaking from overlooked sources.

The turning point was a fraud case:

Logs from external API integrations contained sensitive details such as customer names and addresses.

These logs moved through the network ingress without filtering.

Attackers harvested this data and contacted customers pretending to be official representatives.

Victims were manipulated into sharing OTPs, enabling unauthorized orders, refunds, and scams.

Further investigation revealed:

Multiple APIs were saving PII in plaintext.

Internal-facing apps exposed PII directly in their UI, multiplying the risk surface.

🧩 Key Observations

Logs, APIs, and applications were passing unmonitored customer data.

Attackers didn’t need to breach databases — logs themselves became an entry point.

The existing infrastructure had blind spots that directly enabled fraud.

🔴 Security Gaps Identified

Unfiltered API Logs

No sanitization or masking for sensitive fields.

No real-time alerting when PII was exposed.

Linked to OWASP A09: Logging & Monitoring Failures.

Direct PII Exposure

PII displayed in raw form inside certain internal tools.

Fraud Opportunities

Scammers exploited leaked phone numbers for OTP fraud and refund abuse.

✅ Solution Strategy

🔗 Source Code: detector_full_jui_kalan.py

⚙️ Installation & Usage

Install dependencies:
pip install pandas

Run on Linux:
python3 detector_full_lakshya.py iscp_pii_dataset.csv

Run on Windows:
python detector_full_lakshya.py iscp_pii_dataset.csv

🌍 Why This Matters

Most companies defend their databases but ignore their logs and middleware traffic. This is like locking the safe while leaving confidential documents on your desk.

Every unmasked phone number or address can trigger scams, fines, and loss of user trust.

The proposed tool acts as a real-time guardian, watching every request and response at the network boundary.

Industry Relevance

E-commerce – ISO 27001 compliance

Banking/Finance – PCI DSS compliance

Healthcare – HIPAA compliance

Any domain with regulatory or financial exposure

🛠️ Deployment Design
1. Network & Gateway Layer

Primary deployment at the API Gateway, so every API call is inspected before passing through.

Docker for packaging

Kubernetes for auto-scaling

Prometheus for monitoring

2. Application & Infrastructure Layer

A secondary shield to reinforce protection.

Redis for caching detection rules

PostgreSQL + pgAudit for audit-ready records

ELK Stack for log correlation & alerting

3. DevSecOps Integration

Embedding detection into the CI/CD pipeline ensures vulnerabilities are spotted before release.

SonarQube – Code analysis

OWASP tools – Dependency and image scanning

Trivy – Container vulnerability scans

🖼️ Architecture Overview
<img width="2214" height="3032" alt="Deployment Architecture" src="https://github.com/user-attachments/assets/c855bb80-7496-46c2-a62a-182c32c70e57" />

📌 Addressing Constraints

Latency → Additional ~10ms per request at the API Gateway

Cost → Open-source stack, no licensing fees

Scaling → Kubernetes ensures elasticity with incoming traffic

🏁 Final Thoughts

Placing this solution at the API Gateway transforms security into a proactive shield. It provides:

Enterprise-grade protection

Low operational overhead

Seamless integration into existing infra

Regulatory compliance

This ensures not only technical safety but also business continuity and trust.


Diagrams created using Excalidraw.
