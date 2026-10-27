# Agent Hub: reusable documentation frameworks

These patterns come from the existing project. They are conventions for this project, not a universal agent specification.

## 1. Root README: shared design

- Product Vision: goal and user journey.
- Core Architecture: Hub, Finder, Builder, Executor, Creator, Subagents, Registry.
- Interaction Rules and User-Facing Output Style: communication ownership and presentation.
- Human-in-the-Loop Principle: selection, planning, and execution confirmation.
- Subagent Selection Rules: named-agent validation and alternatives.
- Clarification Rules and Task Complexity Rules: missing information and routing criteria.
- Agent Finder Retrieval and Scoring: retrieval, evaluation, ranking, rationale.
- Execution Result Review: acceptance, modification, retry, or extension.
- Flowcharts and Task Routing Logic: graph and textual paths kept consistent.
- Plain Text Agent Definition Standard: structure, length, and output conventions.
- Planned Repository Structure: file locations.
- Decision Log: date, decision, rationale, status.
- Open Questions: topic, question, options, status.
- Initial Implementation Plan and Milestones: work sequence and completion status.
- Execution Safeguards: scoped behavior and exceptions.

## 2. Role-to-file mapping

| README role | Owned work | Instruction file |
| --- | --- | --- |
| Agent Hub | User interaction, intent, routing, confirmation, final presentation | Agent-Hub.txt |
| Agent Finder | Registry retrieval, fit evaluation, scoring, recommendations | functional-agents/Agent-Finder.txt |
| Workflow Builder | Steps, dependencies, inputs/outputs, approval points | functional-agents/Workflow-Builder.txt |
| Agent Executor | Confirmed scheduling, handoffs, status, exceptions | functional-agents/Agent-Executor.txt |
| Agent Creator | Capability gaps, composition, reuse/adaptation, definition proposals | functional-agents/Agent-Creator.txt |

For each role, check responsibilities, triggers, required inputs, permitted actions, outputs, and handoff boundaries. Similar information may use different subheadings across TXT files.

## 3. Agent definition standard

Top level: Name → Description → Instruction.

Description: concise capability, use trigger, key output or essential limitation. At most 800 characters.

Instruction: role and upstream caller, responsibilities, triggers, input requirements, execution rules, limitations, structured return format. Not every file uses identical nested headings.

Entire TXT: fewer than 8,000 characters. Business agents have English and Chinese names. Missing required inputs must be explicit. Keep metadata aligned with Registry.

## 4. Registry: discovery metadata

Name, Chinese Name, Type, Primary Category, Capability Tags, Domain Tags, Description, Keywords, Capabilities, Use When, Limitations, Permission Level, Status, Last Updated.

One Primary Category per business agent. Fixed permission and status vocabularies. Active means definition completion, not runtime readiness.

## 5. Workflow Blueprint: handoff contract

Task goal, required inputs, assumptions, steps, approval points, capability gaps, execution readiness, confirmation summary.

Per step: step_id, name, responsible_agent, input, output, dependencies, permission_scope, needs_confirmation, expected_result.

This is the actual Builder contract, not a universal format for every agent.

## 6. TODO: progress and verification

Current state → review corrections → repository cleanup → platform setup → permissions and safety checks → functional acceptance → release and maintenance → completion criteria.

Keep completed file checks separate from pending runtime and result validation.

## 7. Submission and test materials

Business value → test scenarios → applicability/reuse → risks and limits → access instructions.

Per test scenario: synthetic inputs, business constraints, request, expected workflow, operating steps, expected results, pass criteria, and actual test records.

## 8. Example instruction to AI

Summarize our accepted roles, responsibilities, workflow branches, and definition standards into the corresponding README sections. Keep unresolved issues in Open Questions. Check each role against its instruction file and identify any inconsistent scope or output. Preserve accepted decisions and report proposed changes for review.

This prompt is illustrative, not a quoted historical conversation.
