# Agentic AI learning projects

Small, practical examples for learning agentic AI and applying it to Microsoft Power Platform and Dynamics 365.

## First project: Case Summary Assistant

A read-only learning prototype for support representatives. It takes case notes and shows a structured draft with known information, unknowns to verify, and suggested next steps.

### Try the demo

Open [the demo page](dynamics-365-case-summary-agent/index.html) in a modern browser. Choose **Use sample case** or enter case text, then select **Summarize case**.

The demo uses simple local text rules, not an AI model. It makes no network requests, does not connect to Dynamics 365, and does not save or send case data.

### What makes the workflow agentic?

1. **Goal:** help a support representative understand a case quickly.
2. **Context:** case title, description, customer impact, and timeline.
3. **Instructions:** summarize only what is present; call out missing information; suggest human-reviewed next steps.
4. **Output:** concise summary with facts, unknowns, and suggestions.
5. **Human review:** the representative decides what to do. The demo cannot update CRM records or contact customers.

This browser demo is deliberately deterministic; it is a UI and workflow teaching aid, not a production AI agent. A real agent needs a model and a controlled data/action connection.

## Map this to Power Platform

A beginner implementation path:

1. In **Copilot Studio**, create an agent named **Case Summary Assistant**.
2. Add an instruction: *Summarize the supplied Dynamics 365 case for a support representative. Use only supplied case data. Separate confirmed facts from unknowns. Suggest next steps for the representative to review. Never claim an action was completed. Do not change case fields or contact the customer.*
3. Start with a manually supplied or mocked case record. Ask the agent to return: **Summary**, **Customer impact**, **Timeline**, **Known facts**, **Unknowns**, and **Suggested next steps**.
4. Once the prompt behaves well, connect it to a narrowly scoped Dataverse/Dynamics 365 knowledge source or Power Automate flow that retrieves one case by ID. Use only the case fields needed for summarization.
5. Keep the first version read-only. If you later add a “draft case note” action, show the draft to the representative and require their approval before saving.
6. Try cases that are complete, ambiguous, and missing key details. Check that the agent identifies unknowns instead of inventing facts.

Exact Copilot Studio and Dataverse setup depends on your tenant, licensing, environment, and permissions.

### Example instruction for a real agent

> You help Dynamics 365 support representatives understand customer service cases. Summarize only the case information provided to you. Do not invent dates, causes, promises, or actions. Clearly label unknown information. Return a brief summary, customer impact, important timeline, known facts, unknowns, and up to three suggested next steps. Suggestions are for the representative to review. You must not update records, send messages, or claim work was completed.

## Safety and scope

- Sample input is fictional.
- The demo runs locally in the browser and makes no network requests.
- It contains no model call and does not access Dynamics 365.
- Do not paste real customer or personal data into prototypes that are not approved for that data.
