# Building Agent Hub with AI

A 21-slide English presentation with a mainly Chinese speaker script. Agent Hub itself is the running project case throughout.

## Files

- `index.html`: the presentation, including inline SVG diagrams and charts.
- `speaker-script.md`: Chinese narration with necessary English technical terms, aligned to all 21 slides.
- `assets/agent-hub-icon.png`: the project logo used inside diagrams.
- `logo.png`: the organization footer logo.

## Slide outline

1. Opening
2. From Chat to Agent Hub: the whole journey at a glance
3. Start with the work, then define the agent roles
4. Agent Hub at the center, with clear functional boundaries
5. Workflow: map the main path, then add decisions
6. Fragment 1: identify what the user wants
7. Fragment 2: find the right agent
8. Fragment 3: break complex work into clear handoffs
9. The complete Agent Hub flow: keep every branch connected
10. Who does what? Follow one confirmed workflow across lanes
11. Inside our README: architecture and definition examples
12. Why this structure? Give each type of information a home
13. From shared standards to one agent definition
14. One routing requirement: define → implement → challenge
15. A file dependency map: one request can affect several files
16. Active is a definition status, not runtime proof
17. A visible loop: decide → develop → review → record
18. Real feedback from this conversation changed the presentation
19. When AI revisits the project: use the diagram as a checkpoint
20. A reusable communication template: design the workflow and README
21. From a conversation to a shared, reviewable design

## Narrative and visual choices

The talk moves from need and roles to workflow, file implementation, review, and a reusable prompt template.

- Roles and the three workflow fragments retain dedicated pages.
- Standards and agent-file behavior are combined into a source-to-definition diagram.
- One routing requirement is traced through its rule, files, and two challenge questions.
- The documented Active correction is combined with definition, runtime, and result validation gates.
- Swimlanes explain responsibility and handoffs. A file-dependency map explains synchronized edits.
- The category bar chart uses 172 business-agent definitions in eight categories, cross-checked against Registry and TXT metadata. It does not describe deployment or performance.
- The circular diagram describes the human–AI iteration loop, not a percentage breakdown.

## Controls and layout

Use arrow keys or navigation buttons to move between slides. F requests full screen. There is no N-key notes overlay.

A fixed 1280 × 720 canvas scales and centers within the preview window. Body text and diagram labels are 16px. Card headings are 16px bold. Source-tree previews are 14px. Footnotes are 12px. The cover has its own typography.

## Evidence boundaries

Content is based on the local Agent Hub README, Agent-Hub.txt, functional and business definitions, Registry, TODO, and test materials.

Prompts and walkthroughs are reconstructed teaching examples unless explicitly tied to a source record. The Active-status correction is recorded in TODO on 2026-10-15. No original conversation or historical Git diff is claimed. File completion, runtime verification, and reviewed results are separate claims.

No screenshots are required by the current version. Original conversations or matching diffs may be added later if available. Existing assets are preserved.

## Rehearsal

Focus on why roles and files were chosen, how workflow decisions become instructions, and how one change is checked. Follow the speaker script rather than reading every label aloud. Confirm timing through rehearsal.

## Logic review

The workflow swimlane follows the three workflow fragments, before file implementation. Its complex-task example explicitly includes candidate selection before blueprint confirmation. The overview allows agent validation as well as Finder discovery. See `logic-chain.md` for the Chinese narrative chain.

## Opening snapshot

Slide 2 replaces the old agenda with Chat → Structured Prompt → Reusable Instructions → Workflow → Agent → Agent Hub. This is a conceptual roadmap, not a strict project chronology or evidence of deployed capability. The deck remains 19 slides.

## Real project artifacts

The README page displays PNG previews rendered from actual Core Architecture and recommended-template text. They are document excerpts, not UI or conversation screenshots. The continuation page displays a viewBox-only crop of the existing Finder SVG, with a link to a preserved full copy. Source project files are unchanged.

Use these artifacts as explicit references in follow-up AI tasks: read current files, identify affected nodes, synchronize changes, and walk through the updated branch. They support review rather than guarantee correctness.

## Opening route-map design

Slide 2 uses a connected six-icon route across three phase bands: clarify the need, make the design reusable, and coordinate capabilities. Each stage includes an action and an artifact, with the real Agent Hub logo at the endpoint. Diagram text remains 16px.

## Complete end-to-end diagram

Slide 9 inserts the existing project end-to-end diagram after the three workflow fragments and before the swimlane. Click its preview to open a scrollable dialog. Use + and − to zoom, Close or Escape to return. Slide-navigation keys do not act while the dialog receives keyboard input.

The copied SVG canvas is expanded to include rightmost and bottommost nodes outside the source viewBox. Diagram content and source project files are unchanged. The full map explains branch connections and design review, not verified runtime behavior.

## Conversation evidence and role-page layout

Slide 19 uses translated feedback from this visible presentation-preparation conversation. The original Chinese excerpts are retained in speaker-script.md. They document editorial iteration, not original Agent Hub development or runtime testing. No other-session chat archive is claimed.

Slide 4 uses a larger relationship diagram and three vertically stacked notes. Its right-side headings and explanations are 14px, with a 12px note. Diagram labels remain 16px.

## Workflow overview layout

Slide 5 uses a taller, tightly framed main workflow on the left and a connected vertical design process on the right: map the path, add decisions, capture rules. Diagram content is unchanged.

## Current slide-specific layout

Slides 4 and 5 use 14px text inside the left diagram and 16px headings and explanations on the right. Slide 9 has a 470px-tall complete-flow preview and four vertically connected stage notes on the right. The full-flow zoom viewer is preserved. These sizes supersede previous slide-specific notes.

## Slide 5 native-scale correction

The left workflow uses its 454 × 370 viewBox at 454 × 370 CSS pixels to avoid enlarging 14px SVG labels. Whole-deck scaling still follows the preview viewport. Right-side text stays 16px.

## Registry chart consolidation

The standalone Registry chart was merged into slide 12, the file-structure rationale. A compact eight-category chart accompanies the need-to-file mapping. Category names are shortened for presentation. Counts remain unchanged. The deck now has 21 slides.

## Architecture grouping and closing

Slide 11 groups the four functional agents beneath functional-agents/, under Agent Hub. Registry and business-subagents/ are sibling resources. This is a reorganized architecture preview, not a verbatim README screenshot. Slide 21 closes with design the logic, preserve shared references, and review changes.

## Restored closing summary

Slide 21 combines the three practical takeaway cards with the original three-sentence closing directly underneath. There is no separate summary slide.

## Practical prompt workshop

Slide 20 replaces the prompt table with a vague-request-to-reviewable-task example: five pieces of task context lead to file changes, branch walkthroughs, and explicit open items. The example refines the existing missing-input contract without claiming historical dialogue, completed changes, or runtime tests.

## Current reusable-template page

Slide 20 restores Goal, Context, Scope, Constraints, and Acceptance. A complete example alongside them asks AI to organize user-request workflows, define agent responsibilities, propose a minimal file structure, and draft the README. It supersedes the earlier missing-input workshop.

## Compact spacing and cover

The cover uses the text title “Building Agent Hub with AI”, without an inline logo. The diagram logos remain. Short question blocks and content cards use content-driven heights rather than forced blank space. Slide 18 no longer pads short feedback quotes to a fixed minimum height.

## Current color semantics

- Blue (#0067B1): chapter labels, structure, references, and neutral library charts.
- Yellow background (#FFF9E6) with dark ochre text (#8A6500): user questions, AI requests, and feedback to address.
- Green (#19734B): corresponding design decisions, file responsibilities, and revised outputs. Green alone does not certify runtime success.
- Gray (#697177 / #F4F6F7): neutral notes and pending verification.

Project-case pages no longer inherit green for all headings. The original project diagram previews retain their purple source-file styling, rather than implying a fourth semantic category in the presentation. Brand-logo colors are preserved.
