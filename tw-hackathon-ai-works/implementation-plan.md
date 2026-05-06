# Implementation plan

## 🏗️ The Technical Stack
* **Frontend:** Next.js or React (Tailwind CSS for speed, **Framer Motion** for sleek transitions).
* **Backend:** Node.js (Express) or Next.js API routes.
* **Database:** PostgreSQL (Supabase) or MongoDB to store session data and "Action Items."
* **AI Engine:** OpenAI (GPT-4o) or Anthropic (Claude 3.5 Sonnet) for the "Judge" and summarization logic.
* **Integrations:** Slack Webhooks (for data input) and Jira API (for "Action Item" export).

## 🛠️ 24-48 Hour Execution Plan

### Phase 1: The "Data Ingest" (Hours 0–6)
* **The Mock Connector:** Instead of fighting with complex OAuth for a 48-hour hack, create a "CSV/JSON Upload" feature where users can drop in a Slack export or Jira log.
* **AI Processing:** Create a prompt that categorizes messages into three buckets: **Wins**, **Frustrations**, and **Technical Debt**.
* **Anonymization Logic:** A function that takes a raw comment like *"John always forgets to update the docs"* and rewrites it to *"Documentation updates are frequently missed in the current workflow."*

### Phase 2: The "Interactive Dashboard" (Hours 6–18)
* **The "Vibe" Chart:** Use **Recharts** or **D3.js** to map out team sentiment over the sprint (e.g., a line graph showing "Stress Levels" vs. "Days to Deadline").
* **The Board UI:** A digital "Sticky Note" board (like Miro/Mural) where the AI has already grouped similar complaints into "Clusters."

### Phase 3: The "AI Judge" & Action (Hours 18–30)
* **The Conflict Resolver:** Build a feature where the AI compares "What the team said" vs. "What the data shows." 
    * *Example:* Team says "We need more meetings," but AI Judge says "Your data shows you already spend 15 hours/week in meetings; the real issue is context switching."
* **Action Item Generator:** A button that takes a summary and formats it into a JSON object ready for a Jira ticket.

## 🎯 High-Impact Features for the Demo

| Feature | The "Wow" Factor |
| :--- | :--- |
| **Sentiment Analysis** | Show a "Live Pulse" of the team that changes color as new feedback is submitted. |
| **AI Clustering** | Drag one sticky note onto another and have the AI instantly generate a "Problem Theme" title for them. |
| **The "Resolution" Bot** | A chat box where the team can ask: *"AI, how do we fix our deployment bottleneck?"* and it cites previous sprint data to give a recommendation. |

## 🎙️ The Winning Pitch Script
1.  **The Hook:** "We spend 20% of our work week in meetings talking about work, rather than doing it. Retrospectives are meant to fix this, but they've become boring, biased, and toothless."
2.  **The Solution:** "Introducing **RetroPulse**. We modernize the retrospective by turning scattered team chatter into actionable, data-backed insights."
3.  **The Demo:** Show the "AI Judge" catching a problem the team missed.
4.  **The Closer:** "RetroPulse doesn't just help teams talk; it helps them **self-heal** by automating the bridge between 'complaint' and 'code'."

## ⚠️ Potential Roadblocks (Avoid These)
* **Don't get stuck on Auth:** Hardcode a single "Team ID" for the demo.
* **Don't over-engineer the integrations:** Use "Mock Data" buttons that simulate a Slack sync if the API is being finicky.
* **Focus on UI/UX:** For a full-stack dev, the judges will expect a polished, "pro" feel. Use a component library like **shadcn/ui** to make it look expensive.


---

The **AI Judge** is the "brain" of RetroPulse. Its job isn't just to summarize; it’s to act as a **data-driven mediator** that identifies cognitive biases and suggests objective fixes.

## 🧠 The Prompt Architecture

You will send a system prompt that defines the Judge's persona. It should be: **Objective, Analytical, and Constructive.**

### 1. The System Role
> "You are the **RetroPulse AI Judge**. Your goal is to analyze team feedback against technical metadata. You don't take sides. You look for 'The Gap'—the difference between how the team *feels* and what the data *shows*. You call out bottlenecks and suggest high-ROI action items."

### 2. The Input Schema
Structure your prompt to feed the AI two specific blocks of data:
* **Block A (Qualitative):** Anonymized team comments (e.g., "The backend is slow," "Requirements are confusing").
* **Block B (Quantitative):** Metadata from Jira/GitHub (e.g., "Average PR review time: 48 hours," "Number of bug tickets: 12," "Sprint Velocity: -20%").

## 📝 The "Master Prompt" Template

Here is the exact structure you can use in your API call:

```markdown
### CONTEXT
We are conducting a sprint retrospective for a software team. 

### TEAM FEEDBACK (Qualitative)
{{anonymized_comments}}

### SPRINT METRICS (Quantitative)
{{jira_github_metrics}}

### YOUR MISSION
Analyze the tension between the feedback and the metrics. Complete the following:

1. **THE REALITY CHECK:** Identify one instance where the team's perception matches the data, and one where it DOES NOT. 
   *(Example: The team feels the DB is slow, but metrics show DB latency is fine; however, API middleware overhead is 3x higher than usual.)*

2. **THE BOTTLENECK:** Pinpoint the single biggest "Self-Healing" opportunity. Where can an automated process replace a manual frustration?

3. **BIAS DETECTION:** Call out any "blame-storming" or logical fallacies in the team comments and rephrase them as systemic issues.

4. **ACTION ITEMS:** Generate 3 specific, non-vague tickets for the next sprint.
```

## ⚖️ Example of the "Judge" in Action

**Team Feedback:** *"We are working too many hours. We need more developers."*
**Jira Data:** *"Total meeting time per developer: 22 hours/week. Average ticket 'Ready for Review' to 'Merged' time: 3 days."*

**The AI Judge Output:**
> "The team reports burnout and requests more headcount. However, the data suggests this is a **Process Bottleneck**, not a **People Bottleneck**. With 55% of the week spent in meetings and code sitting in 'Review' for 3 days, adding more developers will actually *increase* meeting overhead.
> 
> **The Verdict:** Instead of hiring, automate the 'Review' pipeline. 
> **Action Item:** Implement an 'Auto-Assigner' for PRs and block 'No-Agenda' meetings for the next sprint."

## 🛠️ Implementation Tip for the Demo

To make this "pop" in your UI:
1.  **The "Judge's Gavel" UI:** When the user clicks "Run Analysis," show a "Scanning for Biases..." loading state.
2.  **The Highlight Effect:** If the AI Judge disagrees with a team comment, show the comment in red on one side and the Judge's data-backed rebuttal in green on the other. 

**Pro-Tip:** Use **GPT-4o's "JSON Mode"** for this prompt. This ensures the output is always a structured object you can easily map to your React components (e.g., `{ "reality_check": "", "bottleneck": "", "tickets": [] }`).
