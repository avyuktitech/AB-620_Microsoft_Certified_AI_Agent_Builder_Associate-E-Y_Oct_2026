# 🏗️ Architecture & Wiring Diagrams

This section provides the visual architecture, component wiring, conversation flow, and integration diagrams for the Enterprise IT Support AI Agent.

---

# 1. Enterprise AI Agent — Block Diagram

```mermaid
flowchart TB

    U[👤 Employee / User]

    U --> C[🤖 Microsoft Copilot Studio<br/>IT Support Agent]

    C --> GO[🧠 Generative Orchestration]

    GO --> T[💬 Topics & Conversation Flows]
    GO --> K[📚 Knowledge Sources]
    GO --> A[⚙️ Actions / Tools]

    T --> V[📦 Variables & Entities]
    T --> P[🧮 Power Fx]
    T --> B[🔀 Conditions & Branching]
    T --> AC[🃏 Adaptive Cards]

    K --> SP[📁 SharePoint<br/>IT Knowledge Base]
    K --> DOC[📄 Policy / PDF Documents]

    A --> PA[⚡ Power Automate]
    A --> DV[🗄️ Dataverse]
    A --> API[🌐 Enterprise APIs]

    PA --> DV
    PA --> API

    DV --> R[🎫 IT Service / Ticket Data]

    C --> H[👨‍💼 Human IT Support]

    style U stroke-width:2px
    style C stroke-width:3px
    style GO stroke-width:2px
```

---

# 2. Complete Solution Block Diagram

```mermaid
flowchart LR

    subgraph USER["👤 User Layer"]
        EMP[Employee]
        TEAMS[Microsoft Teams]
        WEB[Web / Custom Channel]
    end

    subgraph AGENT["🤖 AI Agent Layer"]
        CS[Copilot Studio]
        ORCH[Generative Orchestration]
        TOPICS[Topics]
        KNOW[Knowledge]
        TOOLS[Tools / Actions]
    end

    subgraph LOGIC["⚙️ Conversation Logic"]
        VAR[Variables]
        ENT[Entities / Slot Filling]
        FX[Power Fx]
        COND[Conditions]
        CARD[Adaptive Cards]
        SYS[System Topics]
        FALL[Fallback]
    end

    subgraph DATA["🗄️ Enterprise Data"]
        DV[Dataverse]
        SP[SharePoint]
        DOCS[Policy Documents]
        KB[IT Knowledge Base]
    end

    subgraph AUTOMATION["⚡ Automation"]
        PA[Power Automate]
        API[Enterprise APIs]
    end

    subgraph SUPPORT["👨‍💼 Support"]
        HUMAN[Human IT Support]
        TICKET[IT Ticket]
    end

    EMP --> CS
    TEAMS --> CS
    WEB --> CS

    CS --> ORCH

    ORCH --> TOPICS
    ORCH --> KNOW
    ORCH --> TOOLS

    TOPICS --> VAR
    TOPICS --> ENT
    TOPICS --> FX
    TOPICS --> COND
    TOPICS --> CARD
    TOPICS --> SYS
    TOPICS --> FALL

    KNOW --> SP
    KNOW --> DOCS
    KNOW --> KB

    TOOLS --> PA
    TOOLS --> DV
    TOOLS --> API

    PA --> DV
    PA --> TICKET

    FALL --> HUMAN
    TICKET --> HUMAN
```

---

# 3. Agent Conversation Wiring Diagram

This diagram shows how a user request travels through the agent.

```mermaid
flowchart TD

    START([👤 User Message])

    START --> INTENT{🧠 Identify Intent}

    INTENT -->|Laptop Request| LAP[Laptop Request Topic]
    INTENT -->|Software Request| SOFT[Software Request Topic]
    INTENT -->|Password Reset| PASS[Password Reset Topic]
    INTENT -->|IT Ticket| TICKET[IT Ticket Topic]
    INTENT -->|Unknown| FALL[Fallback Topic]

    LAP --> SLOT1[📦 Capture Laptop Type]
    SLOT1 --> SLOT2[📦 Capture Business Justification]
    SLOT2 --> SLOT3[📅 Capture Required Date]

    SLOT3 --> FX[🧮 Power Fx]
    FX --> PRIORITY[Calculate Priority]

    PRIORITY --> CONFIRM[🃏 Adaptive Card Confirmation]

    CONFIRM --> DECISION{User Decision}

    DECISION -->|Submit| ACTION[⚡ Create Request]
    DECISION -->|Cancel| CANCEL[❌ Cancel Request]

    ACTION --> SUCCESS[✅ Request Created]
    CANCEL --> END([Conversation End])
    SUCCESS --> END

    SOFT --> SOFTWARE[Collect Application Details]
    SOFTWARE --> APPROVAL[Approval Required]
    APPROVAL --> ACTION2[⚡ Create Software Request]
    ACTION2 --> END

    PASS --> RESET[🔐 Password Reset Guidance]
    RESET --> END

    TICKET --> DETAILS[Collect Issue Details]
    DETAILS --> CREATE[⚡ Create IT Ticket]
    CREATE --> END

    FALL --> CLARIFY[Ask Clarifying Question]
    CLARIFY --> RESOLVE{Intent Identified?}

    RESOLVE -->|Yes| INTENT
    RESOLVE -->|No| HUMAN[👨‍💼 Escalate to Human]
```

---

# 4. Laptop Request — Detailed Wiring Diagram

```mermaid
flowchart TD

    A([User: I need a laptop])

    A --> B[Identify Laptop Request]

    B --> C{Laptop Type}

    C -->|Standard| D[Standard Laptop]
    C -->|Developer| E[Developer Laptop]
    C -->|Executive| F[Executive Laptop]

    D --> G[Capture Reason]
    E --> G
    F --> G

    G --> H[Capture Required Date]

    H --> I[Store Variables]

    I --> J["LaptopType<br/>Reason<br/>RequiredDate"]

    J --> K[Power Fx Calculation]

    K --> L{Priority}

    L -->|High| M[Priority = High]
    L -->|Normal| N[Priority = Normal]

    M --> O[Adaptive Card]
    N --> O

    O --> P{Confirm?}

    P -->|Yes| Q[Power Automate]
    P -->|No| R[Cancel]

    Q --> S[Dataverse / IT Ticket]
    S --> T[Return Ticket Number]

    T --> U([Success])

    R --> V([Conversation End])
```

---

# 5. Knowledge Grounding — Wiring Diagram

```mermaid
flowchart LR

    USER[👤 Employee]

    USER --> AGENT[🤖 Copilot Studio Agent]

    AGENT --> QUERY[User Question]

    QUERY --> SEARCH[🔎 Knowledge Retrieval]

    SEARCH --> SP[📁 SharePoint]
    SEARCH --> PDF[📄 IT Policy PDFs]
    SEARCH --> KB[📚 IT Knowledge Base]

    SP --> RESULTS[Relevant Content]
    PDF --> RESULTS
    KB --> RESULTS

    RESULTS --> GROUND[🧠 Grounded Response]

    GROUND --> AGENT

    AGENT --> USER
```

---

# 6. Power Automate Integration — Wiring Diagram

```mermaid
flowchart LR

    AGENT[🤖 Copilot Studio Agent]

    AGENT --> INPUT[Request Parameters]

    INPUT --> FLOW[⚡ Power Automate Flow]

    FLOW --> VALIDATE[Validate Request]

    VALIDATE --> DECISION{Valid?}

    DECISION -->|No| ERROR[❌ Return Error]

    DECISION -->|Yes| DV[🗄️ Dataverse]

    DV --> TICKET[Create IT Ticket]

    TICKET --> NUMBER[Generate Ticket Number]

    NUMBER --> RESPONSE[Return Response]

    RESPONSE --> AGENT

    AGENT --> USER[👤 Employee]
```

---

# 7. Dataverse Wiring Diagram

```mermaid
erDiagram

    EMPLOYEE ||--o{ IT_REQUEST : creates

    EMPLOYEE {
        string EmployeeID
        string Name
        string Email
        string Department
    }

    IT_REQUEST {
        string RequestID
        string RequestType
        string Description
        string Priority
        string Status
        date RequiredDate
    }

    IT_REQUEST }o--|| IT_CATEGORY : belongs_to

    IT_CATEGORY {
        string CategoryID
        string CategoryName
        string SLA
    }

    IT_REQUEST }o--o| APPROVAL : requires

    APPROVAL {
        string ApprovalID
        string Approver
        string Status
        date ApprovalDate
    }
```

---

# 8. Environment & ALM Wiring Diagram

```mermaid
flowchart LR

    DEV[🛠️ Development Environment]

    DEV --> SOL[📦 Managed Solution Structure]

    SOL --> TEST[🧪 Test / UAT Environment]

    TEST --> APPROVE{Business Approval}

    APPROVE -->|Approved| PROD[🚀 Production Environment]

    APPROVE -->|Rejected| DEV

    PROD --> MON[📊 Monitoring & Evaluation]

    DEV --> DLP1[🛡️ DLP Policy]
    TEST --> DLP2[🛡️ DLP Policy]
    PROD --> DLP3[🛡️ Production DLP Policy]

    DEV --> ENV1[Environment Variables]
    TEST --> ENV2[Environment Variables]
    PROD --> ENV3[Environment Variables]

    DEV --> CON1[Connection References]
    TEST --> CON2[Connection References]
    PROD --> CON3[Connection References]
```

---

# 9. Enterprise Security & Governance Wiring

```mermaid
flowchart TD

    GOVERNANCE[🏢 Enterprise Governance]

    GOVERNANCE --> IAM[🔐 Identity & Access]
    GOVERNANCE --> DLP[🛡️ DLP Policies]
    GOVERNANCE --> ENV[🌐 Environment Strategy]
    GOVERNANCE --> ALM[📦 ALM / Solutions]
    GOVERNANCE --> DATA[🔒 Data Governance]
    GOVERNANCE --> MON[📊 Monitoring]

    IAM --> RBAC[Role-Based Access]
    IAM --> MFA[Identity Controls]

    DLP --> BUSINESS[Business Connectors]
    DLP --> NONBUSINESS[Non-Business Connectors]
    DLP --> BLOCKED[Blocked Connectors]

    ENV --> DEV[Development]
    ENV --> TEST[Test / UAT]
    ENV --> PROD[Production]

    ALM --> SOLUTIONS[Solutions]
    ALM --> CONN[Connection References]
    ALM --> VARIABLES[Environment Variables]

    DATA --> DV[Dataverse]
    DATA --> SP[SharePoint]
    DATA --> API[Enterprise APIs]

    MON --> LOGS[Logs]
    MON --> EVAL[Agent Evaluation]
    MON --> ANALYTICS[Usage Analytics]
```

---

# 10. End-to-End Enterprise Wiring Diagram

This is the **master architecture diagram** for the complete mini-project.

```mermaid
flowchart TB

    USER[👤 Employee]

    USER --> CHANNEL[Microsoft Teams / Web / Channel]

    CHANNEL --> AGENT[🤖 Enterprise IT Support Agent]

    AGENT --> ORCH[🧠 Generative Orchestration]

    ORCH --> INTENT{Intent}

    INTENT --> TOPIC[💬 Topics]
    INTENT --> KNOW[📚 Knowledge]
    INTENT --> TOOLS[⚙️ Tools]
    INTENT --> FALLBACK[🚨 Fallback]

    TOPIC --> VARIABLES[📦 Variables]
    TOPIC --> SLOT[🎯 Slot Filling]
    TOPIC --> FX[🧮 Power Fx]
    TOPIC --> CONDITION[🔀 Conditions]
    TOPIC --> CARD[🃏 Adaptive Cards]

    KNOW --> SP[SharePoint]
    KNOW --> DOCS[Policy Documents]
    KNOW --> KB[IT Knowledge Base]

    TOOLS --> PA[⚡ Power Automate]

    PA --> DV[🗄️ Dataverse]
    PA --> API[🌐 Enterprise API]
    PA --> TICKET[🎫 IT Ticket]

    TICKET --> HUMAN[👨‍💼 IT Support]

    FALLBACK --> HUMAN

    AGENT --> SECURITY[🔐 Security & Governance]

    SECURITY --> DLP[🛡️ DLP]
    SECURITY --> IAM[Identity / Access]
    SECURITY --> ALM[📦 ALM]
    SECURITY --> ENV[🌐 Environments]

    ENV --> DEV[DEV]
    ENV --> TEST[TEST]
    ENV --> PROD[PROD]

    DEV --> TEST
    TEST --> PROD

    PROD --> MONITOR[📊 Monitoring & Evaluation]
```

---

# 11. User Request → AI Agent → Enterprise System

The complete request lifecycle can be summarized as:

```text
┌───────────────────────────────────────────────────────────────┐
│                         USER                                  │
│              "I need a developer laptop"                     │
└────────────────────────────┬──────────────────────────────────┘
                             │
                             ▼
┌───────────────────────────────────────────────────────────────┐
│                    COPILOT STUDIO                             │
│                                                               │
│  Generative Orchestration → Intent → Topic / Tool / Knowledge│
└────────────────────────────┬──────────────────────────────────┘
                             │
                             ▼
┌───────────────────────────────────────────────────────────────┐
│                  CONVERSATION LOGIC                           │
│                                                               │
│ Variables → Slot Filling → Conditions → Power Fx              │
└────────────────────────────┬──────────────────────────────────┘
                             │
                             ▼
┌───────────────────────────────────────────────────────────────┐
│                    USER CONFIRMATION                           │
│                     Adaptive Card                              │
└────────────────────────────┬──────────────────────────────────┘
                             │
                             ▼
┌───────────────────────────────────────────────────────────────┐
│                     POWER AUTOMATE                             │
└────────────────────────────┬──────────────────────────────────┘
                             │
                             ▼
┌───────────────────────────────────────────────────────────────┐
│                       DATAVERSE                                │
│                  IT Request / Ticket                           │
└────────────────────────────┬──────────────────────────────────┘
                             │
                             ▼
┌───────────────────────────────────────────────────────────────┐
│                    IT SUPPORT TEAM                             │
│                       👨‍💼                                    │
└───────────────────────────────────────────────────────────────┘
```

---

# 🔌 Component Wiring Summary

| Source         | Component                | Destination       | Purpose                |
| -------------- | ------------------------ | ----------------- | ---------------------- |
| Employee       | Copilot Studio           | Agent             | User interaction       |
| Agent          | Generative Orchestration | Topics/Tools      | Intent understanding   |
| Agent          | Knowledge                | SharePoint/PDF    | Grounded answers       |
| Topic          | Variables                | Conversation      | Maintain context       |
| Topic          | Power Fx                 | Business Logic    | Calculations           |
| Topic          | Adaptive Card            | User              | Confirmation           |
| Agent          | Power Automate           | Dataverse         | Transaction processing |
| Power Automate | API                      | Enterprise System | Integration            |
| Agent          | Fallback                 | Human Support     | Escalation             |
| Solution       | Connection Reference     | Connector         | ALM                    |
| Environment    | DLP                      | Connectors        | Governance             |
| DEV            | Solution                 | TEST              | Deployment             |
| TEST           | Solution                 | PROD              | Production deployment  |

---

# 🧪 Diagram-Based Validation

Participants should be able to trace the complete flow:

```text
User
 ↓
Channel
 ↓
Copilot Studio
 ↓
Generative Orchestration
 ↓
Intent
 ↓
Topic / Knowledge / Tool
 ↓
Variables
 ↓
Power Fx
 ↓
Condition
 ↓
Adaptive Card
 ↓
Power Automate
 ↓
Dataverse / API
 ↓
IT Ticket
 ↓
Human Support
```

The objective is not only to build the agent but also to understand **how every component is wired together in an enterprise AI solution**.
