# AB-620 – Microsoft Certified: AI Agent Builder Associate

**Training repository | October 2026**  
**Repository:** [AB-620 Training Materials, Labs, Code & Projects](https://github.com/avyuktitech/AB-620_Microsoft_Certified_AI_Agent_Builder_Associate-E-Y_Oct_2026)

Welcome to the AB-620 training repository. This repository brings together day-wise course materials, hands-on labs, code samples, agent workflows, practice questions, exam-preparation resources, mini projects, and capstone projects for learning how to design, build, integrate, test, and manage AI agent solutions using Microsoft Copilot Studio and related Microsoft AI services.

> **Training resource notice:** This is a learning repository. Practice questions, mock papers, sample policies, labs, and projects are for training and self-assessment; they are not official Microsoft exam questions or a guarantee of exam success. Always check the current Microsoft certification page and product documentation for the latest requirements and features.

## Contents

- [Learning path at a glance](#learning-path-at-a-glance)
- [Day-wise course materials](#day-wise-course-materials)
- [Exam preparation](#exam-preparation)
- [Mini projects](#mini-projects)
- [Capstone projects](#capstone-projects)
- [Code, notebooks, and agent workflows](#code-notebooks-and-agent-workflows)
- [Knowledge files and sample resources](#knowledge-files-and-sample-resources)
- [Getting started](#getting-started)
- [Responsible use and security](#responsible-use-and-security)
- [Useful links](#useful-links)

## Learning path at a glance

| Day / area | Focus | Key topics and practice |
|---|---|---|
| Day 1 | Copilot Studio foundations and generative AI | Agent concepts, generative AI fundamentals, agentic RAG, embeddings, chunking, and vector database design |
| Day 2 | Plan and configure agent solutions | Use-case planning, conversational design, environments, governance, DLP, connections, and solution lifecycle concepts |
| Day 3 | Build agents and orchestration | Topics, triggers, generative orchestration, variables, conditions, Power Fx, and conversation design |
| Day 4 | Knowledge, RAG, and agent collaboration | Knowledge sources, retrieval-augmented generation (RAG), Agent-to-Agent (A2A), and sequential/parallel agent workflows |
| Day 5 | Integrate, test, manage, and prepare | Integrations, agent testing and lifecycle, capstone work, and certification readiness |

The day-wise folders contain the available material for each session. Review each folder's own `README.md` for its specific files and instructions.

## Day-wise course materials

- **[DAY1 – Foundations and RAG](DAY1/README.md)**
  - Copilot Studio deep-dive material
  - Agentic RAG block diagrams
  - Vector database design, chunking, and embedding-tuning material
- **[DAY2 – Plan and Configure Agent Solutions](DAY2/README.md)**
  - Agent solution planning, environment strategy, governance, and configuration
- **[DAY3 – Build Agents and Generative Orchestration](DAY3/README.md)**
  - Topics, triggers, and generative orchestration
- **[DAY4 – Knowledge Sources, RAG, and A2A](DAY4/README.md)**
  - Knowledge sources and RAG
  - Agent-to-Agent architecture and use cases
  - Notebook examples and multi-agent workflows
- **[DAY5 – Integrate, Test, Manage, and Capstone Readiness](DAY5/README.md)**
  - Integration and extension material
  - Testing and managing agents
  - Capstone and exam-readiness material

> Some filenames use `AB-650` or `AB_650` in their names while residing in this AB-620 training repository. The names are preserved as uploaded; refer to the content and the relevant folder README for context.

## Exam preparation

- **[AB620-Exam-Guide](AB620-Exam-Guide/README.md)** – exam-guide PDFs and related notes.
- **[AB620-Exam-Papers](AB620-Exam-Papers/README.md)** – practice question sets and MCQs.
- **[Exam outline spreadsheet](AB-620_Microsoft_Certified-AI_Agent%20Builder_Associate.xlsx)** – review the spreadsheet in the repository if you need the supplied outline or mapping.

Use practice material to identify knowledge gaps, then validate product behavior and exam objectives against current Microsoft Learn documentation. Do not treat practice questions as leaked or official exam content.

## Mini projects

- **[Mini-Project1](Mini-Project1/README.md)** – open the project README for the scenario, setup, and tasks.
- **[Mini-Project2](Mini-Project2/README.md)** – open this folder to review the available project files and instructions.
- **[Sequential and Parallel Agent Workflows](DAY4/Notebooks/Mini-Project2-par-seq-orch-agents/README.md)** – demonstrates workflow patterns using Microsoft Agent Framework, Azure AI Foundry, and DevUI.

The sequential workflow illustrates a **Researcher → Writer** pattern. The parallel workflow illustrates a location-selection step followed by parallel destination, weather, and cuisine branches, with an itinerary-planning step to combine results. See the project README and `APPLICATIONLOGIC.md` for implementation details.

## Capstone projects

- **[CAPSTONE-Project1](CAPSTONE-Project1/README.md)** – capstone project brief and supporting PDF.
- The supplied capstone pack includes two enterprise-oriented scenarios:
  1. **Enterprise Employee Service Desk – Multi-Agent AI Solution**
  2. **Intelligent IT Incident Triage & Resolution**

Use the project brief to plan the solution, define agents and hand-offs, identify knowledge sources and tools, implement appropriate security and governance, test scenarios, and prepare a demonstration. Confirm the exact deliverables and acceptance criteria in the project files.

## Code, notebooks, and agent workflows

Browse **[DAY4/Notebooks](DAY4/Notebooks)** for notebook examples and supporting code.

| Resource | Location | Purpose |
|---|---|---|
| A2A client/server notebooks | [`DAY4/Notebooks/A2A`](DAY4/Notebooks/A2A) | Explore a basic Agent-to-Agent client/server example |
| Sequential/parallel workflow project | [`DAY4/Notebooks/Mini-Project2-par-seq-orch-agents`](DAY4/Notebooks/Mini-Project2-par-seq-orch-agents) | Run sequential and parallel agent workflows with DevUI |
| Application logic and wiring | [`APPLICATIONLOGIC.md`](DAY4/Notebooks/Mini-Project2-par-seq-orch-agents/APPLICATIONLOGIC.md) | Understand workflow steps and connections |
| Notebook bundle | [`Notebooks.zip`](DAY4/Notebooks.zip) | Download the supplied notebook bundle |
| A2A notebook bundle | [`Notebooks-A2A.zip`](DAY4/Notebooks/Notebooks-A2A.zip) | Download the supplied A2A notebook bundle |

### Running the sequential/parallel workflow project

Use the project-specific README as the source of truth. The general setup shown there is:

```powershell
python -m venv myvirtualenv
.\myvirtualenv\Scripts\Activate
pip install -r requirements.txt
az login
```

Create a local `.env` file with your own Azure AI Foundry project endpoint and model deployment name. The project README documents the expected variable names, such as:

```dotenv
FOUNDRY_PROJECT_ENDPOINT=https://your-foundry-resource.services.ai.azure.com/api/projects/your-project
MODEL_DEPLOYMENT_NAME=your-model-deployment-name
```

Then, from the project directory, run the workflow you want to test:

```powershell
python .\sequential-workflow-devui.py
```

or:

```powershell
python .\parallel-workflow-devui.py
```

Follow the project README for the DevUI ports, alternate environment-variable names, sample prompts, and troubleshooting guidance. You need an Azure identity with access to the relevant Foundry project and model deployment. Azure resources, model deployments, and permissions are not included with this repository.

## Knowledge files and sample resources

The repository also contains example knowledge and support resources, including:

- Finance policy, expense/reimbursement, invoice/payment, budget analysis, and procurement guides
- Sample HR policy and IT support/security knowledge documents
- Skill files and evaluation conversation templates
- Lab access spreadsheet and other supporting materials

Use the relevant folder README to locate the files. **Treat sample policies, lab credentials, and any employee/vendor examples as training data only.** Do not publish real credentials, secrets, personal data, customer data, or confidential company information in a public repository. Rotate or remove any credential that may have been exposed.

## Getting started

1. **Clone the repository** or download it as a ZIP from GitHub.
2. Start with the day-wise folder matching your current session.
3. Read the folder-level `README.md` before running code or starting a project.
4. Install dependencies only in a virtual environment and review package requirements first.
5. Configure Azure endpoints, deployment names, authentication, and other secrets locally; do not commit `.env` files or credentials.
6. Complete the practice labs and mini projects, then use the capstone briefs to demonstrate an integrated solution.
7. Validate current product steps against the official documentation because Microsoft UI labels, preview features, licensing, and APIs can change.

## Responsible use and security

- Follow your organization's data protection, DLP, identity, and AI governance requirements.
- Use least-privilege access for Azure, Fabric, Power Platform, and Copilot Studio resources.
- Never commit access tokens, passwords, API keys, private certificates, connection strings, or production `.env` files.
- Use synthetic or approved sample data in labs.
- Verify generated outputs and test error handling, permissions, and escalation paths before any production use.
- Check current licensing and regional availability before deploying Microsoft AI features.

## Useful links

- [Repository home](https://github.com/avyuktitech/AB-620_Microsoft_Certified_AI_Agent_Builder_Associate-E-Y_Oct_2026)
- [Microsoft Learn](https://learn.microsoft.com/)
- [Microsoft Copilot Studio documentation](https://learn.microsoft.com/en-us/microsoft-copilot-studio/)
- [Microsoft Fabric documentation](https://learn.microsoft.com/en-us/fabric/)
- [Azure AI Foundry documentation](https://learn.microsoft.com/en-us/azure/ai-foundry/)

## Feedback and contributions

For corrections or improvements, use the repository's Issues or Pull Requests. When contributing, describe the change, include reproducible steps where relevant, and ensure no secrets or confidential information are included.

---

**Maintained by:** [avyuktitech](https://github.com/avyuktitech)  
**Repository:** [AB-620 Microsoft Certified AI Agent Builder Associate – E-Y October 2026](https://github.com/avyuktitech/AB-620_Microsoft_Certified_AI_Agent_Builder_Associate-E-Y_Oct_2026)
