# Coordinator System

*A multi-session coordination system for Claude Code, developed through human–AI collaboration.*

**Created and maintained by [@zx-chai](https://github.com/zx-chai)**

## Overview

**Coordinator** is a custom instruction system designed to organize and manage complex work across multiple Claude Code sessions.

Rather than having one AI session handle planning, execution, and review, Coordinator acts as a central point of coordination.

It helps the user plan work, delegates tasks to specialized sessions, reviews their results, and reports back.

The system follows several principles:

- **Incremental Planning:** Plan one step at a time rather than planning an entire project upfront.
- **Division of Responsibilities:** Assign tasks to sessions with specialized roles.
- **Context Management:** Keep the Coordinator's context focused by delegating substantial work.
- **Quality Control:** Review significant work before considering it complete.
- **User Oversight:** Request approval for proposed plans and involve the user in important decisions.
- **Efficient Model Selection:** Choose models and reasoning effort according to task requirements.

The goal is to make AI-assisted work more organized, efficient, and manageable.

## How the System Works

Coordinator separates managing a project from executing its individual tasks.

The **Coordinator session** handles:

- Understanding the user's goals and requirements
- Discussing ideas and capturing agreed-upon tasks
- Planning the next step
- Starting and managing separate sessions
- Assigning work to specialized roles
- Reviewing results and tracking progress
- Reporting back to the user

The sessions it starts perform the assigned work.

This separation is intended to prevent the Coordinator's context window from becoming unnecessarily filled with implementation details.

### Session Roles

| Role | Responsibility |
|---|---|
| **Researcher** | Gathers information and reports findings without modifying files. |
| **Executor** | Implements tasks, creates deliverables, and makes changes. |
| **Reviewer** | Examines completed work, identifies problems, and checks corrections. |
| **Operator** | Handles mechanical, straightforward, or computer-use tasks. |

The Coordinator manages these sessions and decides when each role is appropriate.

## Requirements

The system is designed for the **Claude app's Claude Code environment**, using its session-management capabilities.

The instructions reference tools such as:

- `start_session`
- `set_session_effort`
- `get_session`
- `set_session_title`

These commands are used by the Coordinator to orchestrate sessions, configure models and reasoning effort, and manage its workflow.

The system is intended for a Claude environment where these capabilities are available.

Compatibility with other Claude interfaces, standalone installations, or different application versions is not guaranteed.

## Installation

Coordinator uses Claude Code's **custom output style** functionality.

The output style serves as a convenient way to activate the Coordinator instructions in a particular session.

It is not intended to be used globally.

There are two ways to install it.

### Option A: Ask Claude Code to Install It

This is the recommended option if your Claude Code environment can access and modify its output-style configuration files.

**Step 1:** Open a normal Claude Code session.

**Step 2:** Copy and send the following prompt:

> I want to install a custom output style called **Coordinator**.
>
> The original instructions are available here:
>
> https://github.com/zx-chai/AI-Prompts/blob/main/Coordinator-System/coordinator.md
>
> Please:
>
> 1. Retrieve the complete contents of `coordinator.md` from the repository.
> 2. Check how custom output styles are installed in my current Claude Code environment.
> 3. Install the instructions as a custom output style named `Coordinator`.
> 4. Preserve the original instructions and YAML frontmatter without rewriting or simplifying them.
> 5. Ensure the style is available in my output style selector.
> 6. **Do not set Coordinator as my default output style.**
> 7. Do not modify my other output styles or unrelated configuration files.
> 8. Verify that the installation succeeded and explain how to activate Coordinator manually.
>
> If you cannot access the repository or modify the required configuration, explain what is preventing installation rather than claiming success.

**Step 3:** Review the installation result.

Confirm that Coordinator is available in your output style selector and that your normal style remains the default.

If Claude cannot complete the installation automatically, use the manual method below.

### Option B: Manual Installation

You can also create the output style yourself.

1. Open Claude Code in the Claude app.
2. Open the output style selector.
3. Choose **New style**.
4. Select the option to create a custom style.
5. Name it `Coordinator`.
6. Open [`coordinator.md`](./coordinator.md).
7. Copy the original instructions into the custom style configuration.
8. Save the style.

If your editor provides a separate field for the style name, description, or other metadata, follow its interface rather than duplicating the YAML frontmatter.

Alternatively, where supported, the custom style can be installed as a Markdown file in the Claude Code user configuration directory:

`~/.claude/output-styles/coordinator.md`

Preserve the original file contents, including the YAML frontmatter.

**Important: Do not set Coordinator as the default output style.**

The Coordinator is meant to operate in its own session.

If configured as the default, separately started sessions may inherit the Coordinator instructions, potentially interfering with their assigned roles.

## How to Use Coordinator

Installing Coordinator and activating Coordinator are two different steps.

You only need to install the output style once, but you activate it whenever you want to start a new coordination session.

### Step 1: Start a New Session

Open a fresh Claude Code session in the Claude app.

**Keep your normal output style selected.**

Do not activate Coordinator yet.

### Step 2: Introduce Your Project

Send an initial message explaining what you want to accomplish.

Include your goals, project background, constraints, preferences, or any other information that may be helpful.

For example:

> Hi! I'd like your help with a project.
>
> My goal is to [describe your goal].
>
> Here's some background information: [provide context].
>
> My main requirements or constraints are [describe requirements].
>
> Please confirm your understanding of the project before we begin.

You can make this initial message as detailed or as simple as necessary.

The purpose is to establish the project context before activating the Coordinator instructions.

### Step 3: Establish Understanding

Allow Claude to respond and acknowledge your initial message.

Clarify any misunderstandings if necessary.

Once Claude understands what you're trying to achieve, proceed to the next step.

### Step 4: Activate Coordinator

1. Open the output style selector at the top of the Claude app.
2. Select **Coordinator**.
3. Continue the conversation.

The session should now follow the Coordinator instructions while retaining the context established during your initial exchange.

**Only the session responsible for coordination should use the Coordinator output style.**

Do not change your global default.

### Step 5: Start Working

You can now discuss ideas, assign tasks, or describe what you want to accomplish.

Coordinator distinguishes between ideas for discussion and tasks that have been agreed upon.

If you provide a goal without specific execution instructions, Coordinator will propose the next step.

When planning is required, it will:

1. Determine what needs to happen next.
2. Identify the sessions required.
3. Choose appropriate models and reasoning effort.
4. Present a proposed plan for your approval.
5. Execute the plan after approval.
6. Review results and report back.

Coordinator generally plans one step at a time, using completed work and new information to guide subsequent decisions.

You can also provide explicit session instructions, as described in `coordinator.md`.

## Managing Sessions

Coordinator follows several session-management principles:

- Reuse existing sessions when their context remains relevant.
- Avoid assigning conflicting file edits to multiple sessions.
- Delegate substantial work rather than filling its own context with implementation details.
- Use specialized sessions for research, execution, review, and mechanical work.
- Wait for session reports instead of repeatedly polling.
- Review significant changes before reporting completion.
- Keep the user informed about completed work and unresolved problems.
- Recommend session compaction when a phase ends or its context is no longer needed.

The complete rules for session management are defined in [`coordinator.md`](./coordinator.md).

## Review and Quality Control

The system includes a structured review process for significant work.

When appropriate, a Reviewer session examines work completed by an Executor.

The Reviewer identifies problems against checkable requirements, and the Executor is responsible for addressing them.

The review process may repeat for several rounds.

Unresolved problems are reported to the user when necessary.

Not every task requires a separate review. Simple mechanical changes, exploratory work, and information-gathering tasks may follow a lighter process.

## Model and Effort Selection

Coordinator includes guidelines for choosing models and reasoning effort according to each task's requirements.

The general objective is to use the least expensive configuration capable of achieving the required quality.

More demanding tasks may justify stronger models or greater reasoning effort.

The detailed selection rules are included in the original Coordinator instructions.

## Limitations

Coordinator is an experimental, instruction-based workflow.

Its effectiveness depends on:

- The capabilities available in the Claude app
- The AI model's ability to follow the instructions
- The clarity of the user's goals and project context
- The reliability of delegated sessions
- The availability of the required session-management tools

The instructions describe intended behavior rather than guaranteed execution.

AI-generated work should still be reviewed, particularly when accuracy, security, or significant consequences are involved.

## Feedback and Contributions

**Constructive criticism and improvement suggestions are strongly encouraged.**

This system was developed through experimentation and collaboration with AI, rather than formal training in computer science or artificial intelligence.

I am interested in identifying its weaknesses and understanding how it can be improved.

If you notice:

- Mistakes or incorrect assumptions
- Inefficient session-management practices
- Unnecessary complexity
- Problems with model or effort selection
- Better approaches to task delegation
- Weaknesses in the review process
- Compatibility issues
- Opportunities to improve reliability or clarity

Please consider opening a GitHub Issue or submitting a Pull Request.

Explanations of *why* a proposed change would improve the system are especially appreciated.

The goal is not simply to collect corrections, but to learn from them.

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

**This README was drafted and revised by ChatGPT, developed by OpenAI**, based on the original Coordinator instructions and workflow explanations provided by @zx-chai.

ChatGPT assisted with organizing the documentation, explaining the system, and preparing installation and usage instructions.

### Disclaimer

Coordinator System is an independent, community-created project.

It is not an official product or feature of Anthropic, Claude, or OpenAI, and is not endorsed by those organizations.

---

**Created by [@zx-chai](https://github.com/zx-chai)**

*An ongoing experiment in making AI-assisted work more organized, efficient, and collaborative.*
