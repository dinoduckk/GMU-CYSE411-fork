# Exercise 1 – Threat Elicitation for a Support Portal

## 1. Problem Description

A company provides a web-based **Customer Support Portal** where logged-in users can create support tickets and view their ticket history.

The system identifies tickets using a simple numerical parameter in the URL:

```
https://support.example.com/ticket/view?id=1001
```

If authorization validation is missing, users may manipulate the parameter to access tickets belonging to other users.

---

## 2. Data Flow Diagram (DFD)

![DFD Support Portal](supportportal.png)

[Download the Threat Model](support_portal_threat_model.tmz)

### DFD Components

| Component | Description |
|---|---|
| External Entity | Customer (User interacting with the portal) |
| Process | View Support Ticket – retrieves and displays ticket data |
| Data Store | Support Ticket Database containing all tickets |
| Data Flow | Request containing the `id` parameter and response containing ticket details |
| Trust Boundary | Between the user's browser (untrusted environment) and the backend server |

---

# 3. Specific Threat Challenge

**Type of Threat:** Information Disclosure (Confidentiality Violation)

Students must identify how a malicious user could manipulate the `id` parameter to access tickets belonging to other users.

---

# 4. Threat Enumeration Table (Student)

| Field | Description |
|------|-------------|
| Actor (Threat Source) | |
| Prerequisites | |
| Actions | |
| Consequence | |
| Affected System Component | |
| Impact | |

---

# 5. Solution Example

| Field | Description |
|------|-------------|
| Actor | Authenticated malicious user |
| Prerequisites | Legitimate access to the portal |
| Actions | Modify the `id` parameter in the request |
| Consequence | Access to other users’ tickets |
| Component | View Support Ticket process |
| Impact | Confidentiality breach exposing personal information |