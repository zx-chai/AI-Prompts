# Coordinator System

*A session coordination system for Claude, developed through human–AI collaboration.*

**Created and maintained by [@zx-chai](https://github.com/zx-chai)**

## Overview

**Coordinator** is a custom instruction system designed to organize and manage work across multiple Claude Code sessions.

Rather than having one AI session handle everything, Coordinator acts as a central point of coordination. It helps the user plan work, delegates tasks to specialized sessions, reviews their results, and reports back.

The system is designed around several principles:

- **Incremental planning:** Plan one step at a time instead of planning an entire project upfront.
- **Division of responsibilities:** Assign different tasks to sessions with specialized roles.
- **Context management:** Keep the Coordinator's context focused by delegating substantial work.
- **Quality control:** Review significant work before considering it complete.
- **User oversight:** Request approval for proposed plans and involve the user in important decisions.
- **Efficient model selection:** Choose models and reasoning effort according to task requirements.

The objective is to make complex, multi-session workflows more structured, manageable, and efficient.

## How the System Works

Coordinator separates the responsibilities of managing a project from performing its individual tasks.

The **Coordinator session** is responsible for understanding the user's goals, planning the next step, starting and managing other sessions, tracking progress, reviewing results, and reporting back.

The sessions it starts are responsible for performing their assigned tasks.

This separation helps prevent the Coordinator from filling its own context window with detailed implementation work.

### Session Roles

The system defines four specialized roles:

| Role | Responsibility |
|---|---|
| **Researcher** | Gathers information, examines existing material, and reports findings without changing files. |
| **Executor** | Performs implementation work, creates deliverables, and makes changes. |
| **Reviewer** | Examines completed work, identifies problems, and verifies corrections. |
| **Operator** | Handles straightforward, mechanical, or computer-use tasks. |

Coordinator assigns and manages these roles according to the work required.

## Setup and Installation

### 1. Create a Custom Output Style

Coordinator uses Claude's custom output-style feature to load its instructions.

**The output style is an activation mechanism, not the system itself.**

1. Open the Claude app.
2. Open the output style selector.
3. Select **New style**.
4. Create a custom style named `Coordinator`.
5. Copy the complete contents of [`coordinator.md`](./coordinator.md) into the custom output-style instructions.
6. Save the style.

Keep the instruction content intact, including its configuration metadata where applicable.

### Important: Do Not Set Coordinator as the Default

**Coordinator is intended to be activated only in the session responsible for coordination.**

Do not configure it as your default output style.

The Coordinator starts other Claude Code sessions to perform delegated work. If Coordinator is configured as the default, those sessions may also inherit its instructions.

This would interfere with the intended separation between the Coordinator and the sessions carrying out its tasks.

The recommended approach is to start a normal session and activate Coordinator manually.

## How to Use Coordinator

### Step 1: Start a New Session

Open a new session in the Claude app using your normal output style.

Do not activate Coordinator immediately.

### Step 2: Introduce Your Project

Send an initial message describing what you want to accomplish.

Include relevant information about the project, your goals, constraints, and anything the Coordinator should understand before beginning.

For example:

> Hi! I'm working on a project and would like your help coordinating it.
>
> My goal is to [describe your goal].
>
> Here's some background information: [provide context].
>
> My main requirements or constraints are [describe requirements].
>
> Please confirm that you understand what I'm trying to accomplish.

The goal of this exchange is to establish context before applying the Coordinator instructions.

### Step 3: Wait for Acknowledgment

Allow Claude to respond and confirm its understanding of the project.

Clarify anything important if necessary.

Once the initial context has been established, proceed to the next step.

### Step 4: Activate Coordinator

1. Open the output style selector at the top of the Claude app.
2. Select **Coordinator**.
3. Continue the conversation.

The session should now follow the Coordinator instructions while retaining the context established during the initial conversation.

**Only activate Coordinator in the session intended to manage the work.**

### Step 5: Begin Coordinating

You can now discuss ideas, assign tasks, or describe deliverables.

Coordinator distinguishes between ideas to discuss and tasks that have been agreed upon.

If you provide a goal without detailed execution instructions, Coordinator will propose the next step.

When planning is required, it will:

1. Determine what work should happen next.
2. Identify which sessions should perform that work.
3. Choose appropriate models and reasoning effort.
4. Present the proposed step for your approval.
5. Execute the approved plan.

Coordinator is designed to plan one step at a time, incorporating results and new information before proposing subsequent steps.

## Working With Sessions

Coordinator uses Claude app session-management capabilities to organize work.

Its instructions reference commands such as:

- `start_session` — Start a session to perform assigned work.
- `set_session_effort` — Adjust a session's reasoning effort.
- `get_session` — Retrieve information about a session.
- `set_session_title` — Set a session's title.

These commands are used in the Claude app environment for which this system was designed.

**Compatibility note:** Availability and behavior may depend on the Claude app version, enabled capabilities, and session environment. The system is not intended to operate unchanged in environments that lack the required session-management tools.

### Session Management Principles

Coordinator is instructed to:

- Reuse sessions when their existing context is relevant.
- Avoid assigning conflicting file edits to different sessions.
- Delegate substantial implementation work rather than doing it itself.
- Review significant changes before reporting completion.
- Wait for assigned sessions to report instead of repeatedly polling them.
- Keep the user informed about results and outstanding work.
- Recommend session compaction when a phase ends or context is no longer needed.

These behaviors are defined in more detail in `coordinator.md`.

## Reviews and Quality Control

The Coordinator System includes a structured review process for significant work.

When appropriate, a Reviewer session examines an Executor's work against specific, checkable requirements.

Problems are identified and passed back for correction.

The review process may repeat for several rounds, with unresolved problems reported to the user if they cannot be satisfactorily addressed.

Not every task requires a review. Simple mechanical changes, exploratory tasks, and information-gathering work may follow a lighter process.

## Model and Effort Selection

Coordinator includes guidelines for choosing AI models and reasoning effort according to each session's role and task.

The general objective is to use the least expensive configuration capable of achieving the required quality.

More demanding work may justify a stronger model or greater reasoning effort.

The exact decision rules are included in the Coordinator instructions.

## Limitations

Coordinator is an experimental, instruction-based workflow.

Its effectiveness depends on factors including:

- The capabilities available in the Claude app.
- The AI model's ability to follow complex instructions.
- The quality and clarity of the user's project context.
- The reliability of delegated sessions.
- The availability of the required session-management tools.

The instructions describe intended behavior; they do not guarantee that every operation will succeed.

AI-generated work should still be reviewed, particularly when accuracy, security, or significant consequences are involved.

## Feedback and Contributions

**Constructive criticism and improvement suggestions are strongly encouraged.**

This system was developed through experimentation and collaboration with AI, not through formal training in computer science or artificial intelligence.

I am interested in understanding how it can be improved.

If you notice:

- Mistakes or incorrect assumptions
- Inefficient session-management practices
- Unnecessary complexity
- Problems with model or effort selection
- Better approaches to task delegation
- Weaknesses in the review process
- Compatibility issues
- Opportunities to make the system more reliable or understandable

Please consider opening a GitHub Issue or submitting a Pull Request.

When suggesting a change, explaining *why* it improves the system is especially helpful.

The goal is not simply to collect corrections but to learn from them.

## License and Attribution

This project is shared under the **Creative Commons Attribution-ShareAlike 4.0 International (CC BY-SA 4.0)** license.

You may use, copy, share, and adapt the licensed material, including commercially, subject to the applicable license terms.

When redistributing the original material or publishing adaptations, you must:

1. Provide appropriate attribution to **[@zx-chai](https://github.com/zx-chai)** for the original material.
2. Link to the original repository: [AI-Prompts](https://github.com/zx-chai/AI-Prompts).
3. Indicate whether modifications were made.
4. Distribute adaptations under the same or a compatible ShareAlike license.
5. Include the applicable license information.

See the repository's [`LICENSE`](../LICENSE) file for the full terms.

*Copyright protection for individual AI-assisted materials may vary by jurisdiction. The license applies to material covered by applicable copyright or related rights.*

## Credits and Acknowledgments

### Coordinator System

**Created and maintained by [@zx-chai](https://github.com/zx-chai).**

The Coordinator System was developed through experimentation and collaboration with AI.

Its design, organization, and ongoing development are directed by @zx-chai with AI assistance.

### Documentation

**This README was drafted by ChatGPT, developed by OpenAI**, based on the Coordinator instructions and workflow explanations provided by @zx-chai.

ChatGPT assisted with organizing the documentation, explaining the system, and presenting its setup and usage instructions.

### Disclaimer

Coordinator System is an independent, community-created project.

It is not an official product or feature of Anthropic, Claude, or OpenAI, and is not endorsed by those organizations.

---

**Created by [@zx-chai](https://github.com/zx-chai)**

*An ongoing experiment in making AI-assisted work more organized, efficient, and collaborative.*
