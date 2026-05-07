The AI Analysis Engine is the brain of RetroPulse. Its job is to take "messy" human communication and "cold" project metadata and find the friction between them.

Here is the architectural breakdown and the prompt engineering strategy to build it.

---

### 1. The Data Pipeline (The "Context Loader")
Before the AI can judge, it needs a clean data object. You’ll create a service that aggregates data into a **Sprint Context** JSON:

* **Slack Data:** Filtered for specific channels. Cleaned of emojis and media links.
* **Jira Data:** Ticket keys, transition timestamps (e.g., how long a ticket stayed in "In Review"), and priority levels.
* **GitHub/GitLab:** PR open-to-merge times and comment counts.

---

### 2. The "Anonymizer" (Tone Normalization)
This engine ensures psychological safety. It doesn't just hide names; it **re-writes** the sentiment to be constructive.

**The Prompt Strategy:**
> "You are a professional workplace mediator. Below is a raw comment from a team member. Rewrite it to remove personal attacks, identifying speech patterns, and emotional vitriol while preserving the core technical or procedural complaint."

* **Input:** *"I'm sick of waiting for Sarah to review my PRs. She takes 3 days and then just leaves a nitpicky comment about semi-colons. It's stalling the whole feature!"*
* **AI Output:** *"There is a perceived bottleneck in the code review process, with turnaround times exceeding 48 hours and a focus on minor syntax rather than logic, which is impacting feature delivery."*

---

### 3. The "AI Judge" (The Insight Engine)
This is the core logic. You use **Triangulation** to compare what the team *thinks* happened vs. what the data *says* happened.

**The Logic Flow:**
1.  **Sentiment Cluster:** Group anonymous complaints into themes (e.g., "Reviews," "Requirements," "Meetings").
2.  **Metadata Correlation:** Check Jira/GitHub for those themes.
3.  **The Verdict:** Generate an insight.

**Example Prompt for the Judge:**
```text
Context: 
- Team Sentiment: 70% of comments mention "Too many meetings."
- Jira Data: Sprint velocity dropped by 20%. Average 'In Progress' time for tickets is 4 days.
- Calendar Data: Team had 15 hours of 'Unscheduled' ad-hoc huddles this week.

Task: 
Analyze the discrepancy. Is the team's complaint valid? What is the root cause?

Output Format:
- Verdict: [Sentence]
- Data Evidence: [Bullet points]
- Suggested Action: [Jira Ticket Title]
```

---

### 4. Technical Implementation (Backend)

I recommend using **LangChain** with **Node.js** for the engine. It allows you to "chain" these steps:

1.  **Input:** Raw Slack/Jira dump.
2.  **Chain 1 (The Extractor):** Pulls out "Friction Points."
3.  **Chain 2 (The Anonymizer):** Cleans the points.
4.  **Chain 3 (The Judge):** Compares points to Jira timestamps.
5.  **Output:** A JSON object that feeds your D3.js frontend.

---

### 5. Ethical Guardrails (Crucial)
To make this "demo-ready" and realistic, your engine must include:
* **PII Scrubbing:** A pre-processor that removes names/emails before the data ever hits the LLM (for privacy compliance).
* **The "Gossip" Filter:** If the AI detects purely personal drama (e.g., "I hate the coffee in the office"), it flags it as "Low Relevance" and excludes it from the stress graph.

**Next Step:** Would you like to see a specific **Python/Node code snippet** for the "Tone Normalizer," or should we talk about how to structure the **Database** to store these insights?