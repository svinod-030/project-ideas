## Project RetroPulse: The AI Team Therapist
RetroPulse is a high-impact project because it solves a universal pain point in software development: the **ineffective retrospective**. By combining data-driven insights with a safe space for communication, it moves the "vibe check" from anecdotal to analytical.

---

### 🛠️ The Technical Blueprint

To bring RetroPulse to life, you'll need a stack that supports real-time interaction and heavy data processing.

| Layer | Technology Recommendation | Why? |
| :--- | :--- | :--- |
| **Frontend** | **Next.js + Tailwind CSS** | Fast routing and easy styling for that "high-energy" dashboard feel. |
| **Visuals** | **Recharts or D3.js** | Recharts is easier for standard heatmaps; D3 is better for custom "Stress Graphs." |
| **Backend** | **Node.js (NestJS)** | Excellent for handling multiple integrations (Slack/Jira) via a modular architecture. |
| **Database** | **PostgreSQL + Prisma** | Reliable relational data for storing "friction points" and historical sprint trends. |
| **Real-time** | **Socket.io** | Essential for the "Interactive Retro" so everyone sees updates simultaneously. |
| **AI Orchestration** | **LangChain** | Perfect for chaining the "Anonymizer" and the "AI Judge" logic together. |

---

### 🧠 The "AI Judge" Logic
This is your project's "secret sauce." To make the AI feel like a legitimate therapist/judge, you should implement a **Triangulation Prompt**:

1.  **Input A:** Anonymous team sentiment (e.g., *"We feel rushed."*).
2.  **Input B:** Hard Metadata (e.g., Jira logs showing 48-hour PR idle times).
3.  **The Analysis:** The AI compares the two. If the team complains about "requirements" but the data shows "idle time," the AI generates the "Truth Bomb" insight.

> **Pro Tip:** Use a "Tone Normalizer" prompt to strip away aggressive language. Transform *"Dave never reviews my code!"* into *"Observation: Code review latency is creating a bottleneck for the frontend team."*

---

### 🚀 Implementation Milestones

#### Phase 1: The Connectors (Data Ingestion)
* Set up **OAuth 2.0** for Jira and Slack.
* Create a "Scraper Service" that fetches messages from a specific channel and tickets from a specific sprint.
* **Privacy Guard:** Implement a regex or AI filter to immediately discard PII (Personally Identifiable Information).

#### Phase 2: The Vibe Engine (Analysis)
* Run sentiment analysis on Slack messages to plot the **Stress Heatmap**.
* Calculate "Cycle Time" and "Lead Time" from Jira to find the actual bottlenecks.

#### Phase 3: The Interactive Retro (UI)
* Build the **Anonymizer Chat**. Use a "masked" UI where users see their own avatar, but others see a generic "Teammate" icon.
* Develop the **Action Item Generator**. When the team agrees on a fix, the AI uses the Jira API to `POST` a new ticket automatically.

---

### 💎 The "Wow" Demo Strategy
To impress judges or stakeholders, don't just show a finished dashboard. Show the **Transformation**:

1.  **The Chaos:** Show a Slack log of a "stressful" Tuesday.
2.  **The Insight:** Click "Analyze" and watch the **Vibe Heatmap** spike into the red. 
3.  **The Resolution:** Use the AI Judge to point out the bottleneck. 
4.  **The Closure:** Click one button to turn the "stress" into a Jira ticket titled *"Optimize Tuesday Deployment Pipeline."*

### Next

[AI Analysis](./AI-analysis.md)