# Agent Architecture & Prompt Engineering Reference

## 1. Agent Architecture & System Design

*   **The Cognitive Framework:** Structure agents around memory (Working, Episodic, Semantic, Procedural) and action (internal vs external).
*   **Reasoning Patterns:**
    *   **ReAct:** Iterative loop of thought, action, observation (real-time/simple tasks).
    *   **Plan-and-Execute:** Separates planning from execution (complex/multi-step tasks).
    *   **Reflection:** Iterative self-refinement before finalizing output.
*   **Subagent Orchestration:** Avoid monolithic agents. Use a Coordinator, Specialist Agents, and an Integration Agent for complex workflows.

## 2. Prompt Engineering Principles

*   **Markdown Structuring:** Always use Markdown (headings, bulleted lists) for clear structure.
*   **Role-Based Definition:** Establish strict boundaries, primary tasks, output formats, and tone.
*   **Task Flow (Chain-of-Thought):** Break tasks into numbered steps. Set explicit checkpoints.
*   **The ICE Method:**
    *   *Instructions:* Direct, specific requests.
    *   *Constraints:* Firm boundaries.
    *   *Escalation:* Clear fallback behaviors.
*   **Strategic Repetition:** Repeat critical instructions at the beginning and end of the prompt.
*   **Example-Based Guidance (Few-Shot):** Build a library of specific examples (input, expected output, validation).

## 3. Tool and Action Design

*   **Clear Naming and Docstrings:** Use verb-noun pairs (e.g., `calculate_price`). Docstrings must detail what it does, when to use it, parameters, and return formats.
*   **Explicit Type Hints:** Always include type hints for parameters and return values.
*   **Graceful Error Handling:** Return informative, actionable error messages so the agent can retry or ask for clarification.

## 4. Evaluation and Refinement

*   **Reasoning Layer:** Evaluate if plans are logical and if the agent adheres to them.
*   **Action Layer:** Measure tool selection accuracy and argument generation.
*   **Execution Layer:** Evaluate end-to-end completion and step efficiency (penalize redundant loops).
