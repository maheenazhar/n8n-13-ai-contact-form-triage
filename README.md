# ⚡ AI Contact Form Triage & Routing (Groq + Supabase + Gmail)

[![n8n workflow](https://img.shields.io/badge/n8n-Workflow-orange.svg)](https://n8n.io)
[![Sequence](https://img.shields.io/badge/Sequence-%2313-blue.svg)](#)
[![Difficulty](https://img.shields.io/badge/Difficulty-Advanced-green.svg)](#)
[![Status](https://img.shields.io/badge/Status-Production--Ready-brightgreen.svg)](#)

> **Workflow Sequence #13** in the [Maheen Azhar n8n Workflow Collection](https://github.com/maheenazhar/n8n-workflows-collection).

---

## 📖 Overview

Ingests website contact forms via webhook, sanitizes input fields, uses Groq AI to classify inquiry intent & sentiment, persists the classified ticket in Supabase, and conditionally triggers urgent admin email alerts for high-priority tickets.

### 🎯 Key Use Case
Automated customer support routing, urgent issue escalation, and centralized lead capture with AI sentiment classification.

---

## 🏗️ Architecture & Flow

```mermaid
graph TD
  N0_Trim_Fields["Trim Fields<br><i>(code)</i>"]
  N1_Webhook1["Webhook1<br><i>(webhook)</i>"]
  N2_Prepare_AI_Request1["Prepare AI Request1<br><i>(code)</i>"]
  N3_Groq_Classify1["Groq Classify1<br><i>(httpRequest)</i>"]
  N4_Parse_AI_Result1["Parse AI Result1<br><i>(code)</i>"]
  N5_Save_to_Supabase1["Save to Supabase1<br><i>(supabase)</i>"]
  N6_Needs_Admin_1["Needs Admin?1<br><i>(if)</i>"]
  N7_Alert_Admin1["Alert Admin1<br><i>(gmail)</i>"]
  N0_Trim_Fields --> N5_Save_to_Supabase1
  N1_Webhook1 --> N2_Prepare_AI_Request1
  N2_Prepare_AI_Request1 --> N3_Groq_Classify1
  N3_Groq_Classify1 --> N4_Parse_AI_Result1
  N4_Parse_AI_Result1 --> N0_Trim_Fields
  N5_Save_to_Supabase1 --> N6_Needs_Admin_1
  N6_Needs_Admin_1 --> N7_Alert_Admin1
```

---

## 🧩 Nodes in this Workflow

| # | Node Name | Type | Version |
|---|-----------|------|---------|
| 1 | **Trim Fields** | `n8n-nodes-base.code` | v2 |
| 2 | **Webhook1** | `n8n-nodes-base.webhook` | v2 |
| 3 | **Prepare AI Request1** | `n8n-nodes-base.code` | v2 |
| 4 | **Groq Classify1** | `n8n-nodes-base.httpRequest` | v4.2 |
| 5 | **Parse AI Result1** | `n8n-nodes-base.code` | v2 |
| 6 | **Save to Supabase1** | `n8n-nodes-base.supabase` | v1 |
| 7 | **Needs Admin?1** | `n8n-nodes-base.if` | v2.2 |
| 8 | **Alert Admin1** | `n8n-nodes-base.gmail` | v2.1 |

---

## 🔑 Prerequisites & Credentials

Before running this workflow, ensure you have the following configured in your n8n environment:

- [ ] **Groq API Key**
- [ ] **Supabase credentials & contact_tickets table**
- [ ] **Gmail credential**
- [ ] **Website webhook form integration**

> [!NOTE]
> All credentials are decoupled from this export file for security. When importing into your n8n workspace, re-assign your local credentials in the respective node configuration panels.

---

## 🚀 Setup & Installation

1. **Clone or Download:**
   ```bash
   git clone https://github.com/maheenazhar/n8n-13-ai-contact-form-triage.git
   cd n8n-13-ai-contact-form-triage
   ```
2. **Import into n8n:**
   - Open your n8n canvas.
   - Click the top-right menu `...` -> **Import from File**.
   - Select `workflow.json` from this repository.
   - *(Alternative)*: Open `workflow.json`, copy the entire JSON contents, and paste directly (`Ctrl+V`) onto the n8n canvas.
3. **Configure Credentials:**
   - Open each integration node marked with a red credential prompt.
   - Select or configure your accounts (e.g., Google OAuth, Groq API, Supabase, SMTP).
4. **Activate / Test:**
   - Click **Test step** or **Execute Workflow** to verify end-to-end functionality.
   - Toggle the workflow to **Active** for live production use.

---

## 📄 File Structure

```
13-ai-contact-form-triage/
├── workflow.json   # Full exportable n8n workflow definition
├── README.md       # Comprehensive documentation and architecture
└── .gitignore      # Standard Git exclusions
```

---

## 👤 Author & Repository

- **Author:** [Maheen Azhar](https://github.com/maheenazhar)
- **Workflow ID:** `2nCib93JoKTvfxKI`
- **Created Date:** `2026-10-10 14:04:50.387`
- **Last Modified:** `2026-10-16 02:27:44.640`
- **Repository:** [`https://github.com/maheenazhar/n8n-13-ai-contact-form-triage`](https://github.com/maheenazhar/n8n-13-ai-contact-form-triage)

---

*Part of the [n8n Workflows Collection](https://github.com/maheenazhar/n8n-workflows-collection) by Maheen Azhar.*
