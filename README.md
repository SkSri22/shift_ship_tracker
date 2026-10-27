# SwiftShip Tracker 

**SmartBridge Capstone Project**   
**Institution:** Jaya Engineering College and Technology  
**Team ID:** `SWTID-2026-8823`  

### 👥 Team Members
* **Sriganeshan S K** (Team Lead)
* **I Tharun Kumar**
* **P Ramkumar**
* **Pugazhendhi S**
* **M Rajadurai**

---

## 📺 Project Demonstration Video

**Click the link below to view the live project demonstration:**

👉 [**https://youtu.be/p2jypylErrs?si=Nl_r8rPP5xV1-Sq9**](YOUR_YOUTUBE_UNLISTED_LINK_HERE)

---

## 📖 Project Overview & Scope

**SwiftShip Tracker** is a scalable, end-to-end parcel management CRM built on Salesforce. It automates parcel bookings, shipment updates, sender and receiver details, and delivery operations. Integrated with **Salesforce Agentforce AI** and **Prompt Builder**, it provides real-time, grounded parcel tracking capabilities via an interactive conversational assistant.

### Objectives Summary
* **Automate Parcel Operations:** Streamline booking, tracking, and delivery notifications to reduce manual updates.
* **Enhance Customer Experience:** Provide transparent, real-time status updates through AI self-service tracking.
* **Centralize Operations:** Equip delivery agents and support staff with guided Flows and centralized dashboards.
* **Data Insights:** Deliver operational visibility using custom Salesforce reports and performance dashboards.
* **Enterprise Security:** Ensure role-based access security using Salesforce Role Hierarchies, Profiles, Field-Level Security (FLS), and Permission Sets.

---

## 🛠️ Technology Stack & Key Salesforce Features

* **Platform:** Salesforce Service Cloud / Developer Org
* **Custom Objects:** `Parcel__c`, `Delivery__c`, `Sender__c`, `Receiver__c`
* **Standard Objects:** `Account`, `Contact`, `Case`, `Task`, `EmailMessage`, `User`
* **Automation:** Autolaunched Flows (executed in *System Context Without Sharing*), Record-Triggered Flows
* **AI & Intelligence:** Salesforce Agentforce (Einstein Service Agent), Prompt Builder (Flex / Field Generation Templates)
* **UI & Navigation:** Lightning App Page (*SwiftShip Tracker App*), Custom Object Tabs, Dynamic Forms
* **Security & Governance:** Profiles, Permission Sets (`Parcel Tracker Agent Access`), Role Hierarchies, Field-Level Security

---

## 🗄️ Data Model Architecture

| Custom Object | API Name | Description | Key Fields & Relationships |
| :--- | :--- | :--- | :--- |
| **Parcel** | `Parcel__c` | Core parcel tracking record | `Parcel_ID__c` (Auto-Number: `P-{000}`), `Status__c` (Picklist), `Weight__c` (Number), `Estimated_Delivery_Date__c` (Date), Lookup to `Sender__c` & `Receiver__c` |
| **Delivery** | `Delivery__c` | Delivery status & location logs | `Current_Location__c` (Geolocation), `Estimated_Delivery__c`, Lookup to `Parcel__c` and `Sender__c` |
| **Sender** | `Sender__c` | Origin contact & shipping details | `Sender_Address__c` (Geolocation/Text), `Sender_Contact__c` (Phone), `Sender_Email__c` (Email) |
| **Receiver** | `Receiver__c` | Destination contact details | `Receiver_Address__c` (Geolocation/Text), `Receiver_Contact__c` (Phone), `Receiver_Email__c` (Email), Lookup to `Parcel__c` |

---

## 🚀 Phase-by-Phase Implementation Journey

### **PHASE 1: Project Scope, User Needs & System Architecture**

* **Defining Project Scope & Objectives** *(Assigned to: Sriganeshan S K)*
  * Defined end-to-end parcel lifecycle management (Booking → Dispatch → Tracking → Delivery Confirmation).
  * Established requirements for role-based security, automated notifications, and AI conversational support.

* **Gathering & Analysing User Needs** *(Assigned to: I Tharun Kumar)*
  * Mapped key user personas: Customers/Senders, Delivery Agents, Customer Support Team, System Administrators.
  * Identified functional requirements: real-time status updates (`Booked` → `In Transit` → `Out for Delivery` → `Delivered`), automated email alerts, and Prompt Builder AI integration.

* **Identifying Key Salesforce Features & Tools Required** *(Assigned to: P Ramkumar)*
  * Planned standard & custom object mappings, Lightning App structure, Apex automation needs, and security controls.

* **Designing Data Model and Security Model** *(Assigned to: Pugazhendhi S)*
  * Designed data schema for `Parcel__c`, `Delivery__c`, `Sender__c`, and `Receiver__c`.
  * Designed Role Hierarchy (`Administrator` → `Delivery Manager` → `Agent` → `Customer`) and profile access controls.

---

### **PHASE 2: Declarative Setup, Objects, Automation & AI**

* **Milestone 1 — Salesforce Account & Org Setup** *(Assigned to: M Rajadurai)*
  * Provisioned and configured the Salesforce Developer Org environment.

* **Milestone 2 — Custom Object Creation** *(Assigned to: Sriganeshan S K)*
  * Created custom objects with history tracking, search, and reporting enabled: `Parcel__c`, `Sender__c`, `Receiver__c`, and `Delivery__c`.

* **Milestone 3 — Custom Navigation Tabs** *(Assigned to: I Tharun Kumar)*
  * Generated custom object tabs for `Parcel`, `Delivery`, `Sender`, and `Receiver` and added them to the SwiftShip Tracker App navigation menu.

* **Milestone 4 — Fields & Relationships Configuration** *(Assigned to: P Ramkumar)*
  * Configured field types, auto-number formats (`P-{000}`), picklists, geolocations, and object relationships across all custom objects.

* **Milestone 5 — Prompt Builder & Agentforce Grounding** *(Assigned to: Pugazhendhi S)*
  * Configured Prompt Template `Retrieve_Parcel_Details` linked to `Parcel__c`.
  * Created autolaunched Flow `Get_Parcel_Status` (Input: `Parcel_ID_Input`) running in *System Context Without Sharing*.
  * Bound Flow action to the `# Parcel Tracker` topic in Agentforce Builder.

---

### **PHASE 3: Security Governance, System Context & Access Controls**

* **Permission Set Creation** *(Assigned to: Sriganeshan S K)*
  * Created the `Parcel Tracker Agent Access` Permission Set to manage object permissions and Field-Level Security (FLS).
* **Agent User Assignment** *(Assigned to: I Tharun Kumar)*
  * Assigned the `Parcel Tracker Agent Access` Permission Set to the `EinsteinServiceAgent` user.
* **System Context Configuration** *(Assigned to: P Ramkumar)*
  * Set up autolaunched Flow permissions to execute in *System Context Without Sharing*, enabling safe data lookup while maintaining strict record-level security across roles.

---

### **PHASE 4: Agentforce Fine-Tuning, Prompt Template Integration & Workflow Orchestration**

* **Agentforce Topic & Action Mapping** *(Assigned to: Pugazhendhi S)*
  * Configured `# Parcel Tracker` topic in Agentforce Builder and integrated the `Get_Parcel_Status` autolaunched Flow as a core action.
* **Prompt Builder Grounding** *(Assigned to: M Rajadurai)*
  * Formatted response templates to force exact field mapping from CRM query outputs:
    ```text
    📦 Parcel Tracking Update
    - Parcel Name: {!$Input:Parcel__c.Name}
    - Parcel ID: {!$Input:Parcel__c.Parcel_ID__c}
    - Status: {!$Input:Parcel__c.Status__c}
    - Weight: {!$Input:Parcel__c.Weight__c}
    - Estimated Delivery Date: {!$Input:Parcel__c.Estimated_Delivery_Date__c}
    ```
* **AI Hallucination Prevention** *(Assigned to: Sriganeshan S K)*
  * Added guardrails in Prompt Builder to restrict Agent responses strictly to verified Salesforce Flow data.

---

### **PHASE 5: Live Simulator Testing, Deliverables & Final Submission**

* **Simulator Validation & Test Queries** *(Assigned to: Team All)*
  * Created sample test record **`P-001`** (Weight: `5.5 kg`, Status: `In Transit`, Estimated Delivery: `October 25, 2026`).
  * Validated three real-time interaction scenarios:
    1. **Valid Query:** `"give me the parcel details of P-001"` (Fetches and displays live CRM metrics).
    2. **Invalid Query:** `"Track parcel ID P12345"` (Handles non-existent records gracefully).
    3. **Update Query:** `"Update delivery status for parcel P67890 to Delivered"` (Triggers identity verification safeguards).
* **Deliverables & SkillWallet Submission** *(Assigned to: Sriganeshan S K)*
  * Updated Kanban board cards (`To Do` → `In Progress` → `Review`).
  * Generated project documentation, presentation materials, and thumbnail assets.
  * Uploaded GitHub repository link and YouTube demonstration video link via SkillWallet portal.

---

## 🏁 Conclusion

The **SwiftShip Tracker** project successfully demonstrates a fully functional, end-to-end integration of Salesforce CRM, custom object relationships, system-context Flow automation, Prompt Builder grounding, and Agentforce AI. The solution automates parcel tracking inquiries effectively while upholding enterprise data security and governance.
