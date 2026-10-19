# Building Smarter Agents with Reflection and Planning

An English-language, live-demo-first Jupyter tutorial using **Microsoft Foundry prompt agents (Agents v2) with the Responses API**. It demonstrates baseline, **plan → act**, and **act → critique → revise** using a small, objectively checkable fictional procurement dataset.

## Open in GitHub Codespaces

1. Push this folder to a GitHub repository; ensure `.devcontainer/devcontainer.json` is included.
2. On GitHub select **Code → Codespaces → Create codespace on main**. Dependencies and Azure CLI install automatically.
3. In the Codespaces terminal: `az login --use-device-code` (select the Azure tenant/subscription with your Foundry project).
4. `cp .env.example .env` then edit `.env` (do **not** commit it). Paste your Foundry **project endpoint** and deployed **model name**.
5. Open `notebooks/reflection_planning_tutorial.ipynb`, choose the **Python (Reflection Lab)** kernel and run cells in order.

## Local environment

```bash
python -m venv .venv
source .venv/bin/activate        # Windows PowerShell: .venv\Scripts\Activate.ps1
pip install -r requirements.txt
az login
cp .env.example .env
jupyter lab
```

## Required Azure resources

- A Microsoft Foundry project supporting current Agent Service prompt agents (v2)
- A deployed model usable by that project (put **deployment name**, not model family name, in `.env`)
- Microsoft Entra credentials with sufficient permissions to create agent versions and invoke the deployment

## What the code uses

- `project.agents.create_version(..., PromptAgentDefinition(...))`
- `project.get_openai_client().responses.create(input=..., extra_body={"agent_reference": ...})`
- `previous_response_id` for plan/execution and draft/revision response chaining
- A separate critic whose *visible critique* is passed to the writer; it does not rely on hidden shared memory

## Notes

Running the notebook creates four Foundry agent versions. Cleanup code is provided but is intentionally disabled. Live responses and token usage vary. The lab does not call real vendor APIs and is not a production security or compliance decision system.

**Source:** [Microsoft Learn – reflection and planning cycles, Agents v2](https://learn.microsoft.com/en-us/training/modules/aaai-design-agentic-loops-azure-ai-agent-service/4-implement-agent-reflection-planning-cycles).
