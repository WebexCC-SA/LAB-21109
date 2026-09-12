### Quality Managment Feature Overview

The **Evaluations** feature lets supervisors create customized evaluation forms to assess
human agent and AI Agent interactions automatically. Using AI, interactions are analyzed and
evaluation scores are generated against the pre-defined criteria set by the supervisors.
Supervisors have the ability to manually adjust scores if necessary. When scores are
adjusted, this information is subsequently used to improve the AI models. Evaluation scores
are available both at the individual interaction level and as aggregated data for each agent,
offering clear insights into performance trends. This streamlines quality assurance,
providing consistent and objective feedback and helps maintain high service standards.

## Story

The supervisor requires both the human agent and the AI Agent to always ask for the customer’s name and the occasion for the flowers. Based on these criteria, they will be evaluated and additional training will be provided.

## Call Flow Overview

1. The supervisor logs in to the Supervisor Dashboard, which is configured with Evaluation Forms for human agents and AI Agents.
2. A new call enters the voice flow; the caller asks the AI agent to be connected to a human agent.
3. The human agent talks to the customer about the flower order.
4. After the call is completed, the supervisor checks if the human agent completed the questions based on the Evaluation Form.
5. A separate call is handled entirely by the AI Agent.
6. After that call is completed, the supervisor checks if the AI Agent asked the required questions based on the Evaluation Form assigned to the AI Agent.
