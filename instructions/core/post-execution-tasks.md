---
description: Rules to finish off and deliver to user set of tasks that have been completed using Agent OS
globs:
alwaysApply: false
version: 1.0
encoding: UTF-8
---

# Task Execution Rules

## Overview

Follow these steps to mark your progress updates, create a recap, and deliver the final report to the user.

<pre_flight_check>
  EXECUTE: @.agent-os/instructions/meta/pre-flight.md
</pre_flight_check>

<process_flow>

<step number="1" name="test_suite_verification">

### Step 1: Run All Tests

Run the entire test suite (using your tool's helper or the CLI) to ensure no regressions remain. Fix any failures before continuing.

<instructions>
  ACTION: Execute the full test suite command
  CAPTURE: Failures with file/line references and summarize fixes
  REPEAT: Until all tests pass without intervention
</instructions>

<test_execution>
  <order>
    1. Run entire test suite
    2. Fix any failures
  </order>
  <requirement>100% pass rate</requirement>
</test_execution>

<failure_handling>
  <action>troubleshoot and fix</action>
  <priority>before proceeding</priority>
</failure_handling>

</step>

<step number="2" name="git_workflow">

### Step 2: Git Workflow

Create a clean git commit, push your branch, and prepare a pull request for the implemented features. Use automated helpers if available or run the git commands manually.

<instructions>
  ACTION: Stage changes (`git add`), commit with a descriptive message, and push to the remote branch
  OPTIONAL: Open a PR draft or create the PR with summary/test notes
  RECORD: Keep the PR URL for the completion summary
</instructions>

<commit_process>
  <commit>
    <message>descriptive summary of changes</message>
    <format>conventional commits if applicable</format>
  </commit>
  <push>
    <target>spec branch</target>
    <remote>origin</remote>
  </push>
  <pull_request>
    <title>descriptive PR title</title>
    <description>functionality recap</description>
  </pull_request>
</commit_process>

</step>

<step number="3" name="tasks_list_check">

### Step 3: Tasks Completion Verification

Review the spec’s `tasks.md` and confirm that all tasks are marked complete (`[x]`) or clearly documented as blocked (with `⚠️`). Update the file manually if anything is missing.

<instructions>
  ACTION: Open `.agent-os/specs/<spec-folder>/tasks.md`
  CHECK: Ensure every parent task and subtask is marked `[x]` when complete
  BLOCKERS: If work remains after three attempts, note `⚠️ Blocking issue: ...`
  UPDATE: Save the file with the latest status for future runs
</instructions>

</step>

<step number="4" name="roadmap_progress_check">

### Step 4: Roadmap Progress Update (conditional)

Check @.agent-os/product/roadmap.md and mark items complete (`[x]`) only if the executed tasks fulfill the roadmap milestone. Update notes as needed.

<conditional_execution>
  <preliminary_check>
    EVALUATE: Did executed tasks complete any roadmap item(s)?
    IF NO:
      SKIP this entire step
      PROCEED to step 5
    IF YES:
      CONTINUE with roadmap check
  </preliminary_check>
</conditional_execution>

<roadmap_criteria>
  <update_when>
    - spec fully implements roadmap feature
    - all related tasks completed
    - tests passing
  </update_when>
</roadmap_criteria>

<instructions>
  ACTION: First evaluate if roadmap check is needed
      SKIP: If tasks clearly don't complete roadmap items
  EVALUATE: If current spec completes roadmap goals
  UPDATE: Mark roadmap items complete with [x] if applicable
</instructions>

</step>

<step number="5" name="document_recap">

### Step 5: Create Recap Document

Create a recap document in `.agent-os/recaps/` summarizing what was built, referencing the spec folder and spec-lite summary.

<instructions>
  ACTION: Create `.agent-os/recaps/[SPEC_FOLDER_NAME].md`
  TEMPLATE: Use the recap template below and link back to the spec folder
  CONTENT: Summarize outcomes, include key bullet points, reference spec-lite context
  VERIFY: Confirm the recap accurately reflects shipped work
</instructions>

<recap_template>
  # [yyyy-mm-dd] Recap: Feature Name

  This recaps what was built for the spec documented at .agent-os/specs/[spec-folder-name]/spec.md.

  ## Recap

  [1 paragraph summary plus short bullet list of what was completed]

  ## Context

  [Copy the summary found in spec-lite.md to provide concise context of what the initial goal for this spec was]
</recap_template>

<file_creation>
  <location>.agent-os/recaps/</location>
  <naming>[SPEC_FOLDER_NAME].md</naming>
  <format>markdown with yaml frontmatter if needed</format>
</file_creation>

<content_requirements>
  <summary>1 paragraph plus bullet points</summary>
  <context>from spec-lite.md summary</context>
  <reference>link to original spec</reference>
</content_requirements>

</step>

<step number="6" name="completion_summary">

### Step 6: Completion Summary

Prepare a structured summary message (using the template below) that covers what was done, issues encountered, testing steps, and includes the PR link.

<summary_template>
  ## ✅ What's been done

  1. **[FEATURE_1]** - [ONE_SENTENCE_DESCRIPTION]
  2. **[FEATURE_2]** - [ONE_SENTENCE_DESCRIPTION]

  ## ⚠️ Issues encountered

  [ONLY_IF_APPLICABLE]
  - **[ISSUE_1]** - [DESCRIPTION_AND_REASON]

  ## 👀 Ready to test in browser

  [ONLY_IF_APPLICABLE]
  1. [STEP_1_TO_TEST]
  2. [STEP_2_TO_TEST]

  ## 📦 Pull Request

  View PR: [GITHUB_PR_URL]
</summary_template>

<summary_sections>
  <required>
    - functionality recap
    - pull request info
  </required>
  <conditional>
    - issues encountered (if any)
    - testing instructions (if testable in browser)
  </conditional>
</summary_sections>

<instructions>
  ACTION: Create comprehensive summary
  INCLUDE: All required sections
  ADD: Conditional sections if applicable
  FORMAT: Use emoji headers for scannability
</instructions>

</step>

<step number="7" name="completion_notification">

### Step 7: Task Completion Notification

Play a completion notification (e.g., `afplay /System/Library/Sounds/Glass.aiff` on macOS) or send an equivalent alert to signal the human operator that work is finished.

<notification_command>
  afplay /System/Library/Sounds/Glass.aiff
</notification_command>

<instructions>
  ACTION: Play completion sound
  PURPOSE: Alert user that task is complete
</instructions>

</step>

</process_flow>

<post_flight_check>
  EXECUTE: @.agent-os/instructions/meta/post-flight.md
</post_flight_check>
