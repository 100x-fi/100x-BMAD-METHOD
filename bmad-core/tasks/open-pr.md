<!-- Powered by BMAD™ Core -->

# open-pr

Draft a pull request description for the current branch, linking to the specified story and its associated GitHub issue.

## Purpose

Generate a comprehensive pull request description that:

- Links to the story file and its associated GitHub issue
- Provides context about the changes made
- Follows project conventions for PR descriptions
- Enables proper GitHub issue tracking and closure

## Prerequisites

- Current branch contains story implementation
- Story file exists in `devStoryLocation` with GitHub Issue section
- Git repository is properly configured
- GitHub CLI (`gh`) is available (optional, for enhanced functionality)

## Task Execution Instructions

### 1. Execute Linting and Tests

Before proceeding with PR creation:

- Run linting to ensure code quality standards are met
- Execute all tests to verify functionality
- Fix any linting errors or test failures before continuing
- HALT if linting or tests fail and inform user of the issues

### 2. Load Story Information

- Load story file from pensri-docs repository: `100x-fi/pensri-docs/docs/stories/{story-number}.story.md`
- Extract story title, acceptance criteria, and implementation details
- Locate "GitHub Issue" section and extract the issue number (e.g., "#173")
- Read "Dev Agent Record" section for implementation notes and file changes

### 3. Auto-Populate from Dev Agent Record

- Extract implementation details from "Dev Agent Record" section
- Get "Completion Notes List" for change summary
- Extract "File List" for modified/added files
- Use "Debug Log References" for testing status
- Get "Agent Model Used" for context

### 4. Generate PR Description

Create a structured PR description auto-populated from Dev Agent Record:

```markdown
## Story Implementation

**Story:** {story-number} - {story-title}
**Story File:** [{story-number}.story.md](link-to-story-file)

## Changes Made

### Summary

{Extract from Dev Agent Record "Completion Notes List"}

### Key Changes

- {Auto-populate from "Completion Notes List"}
- {Auto-populate from "File List" - new files}
- {Auto-populate from "File List" - modified files}

### Acceptance Criteria Met

- [x] {AC1 description}
- [x] {AC2 description}
- [x] {AC3 description}

## Testing

- [x] Unit tests added/updated (from Debug Log References)
- [x] Integration tests pass (from Debug Log References)
- [x] Manual testing completed (from Debug Log References)
- [x] No regression in existing functionality

## Files Changed

{List of files from Dev Agent Record File List section}

## GitHub Issue

Closes 100x-fi/pensri-docs#{issue-number} - {issue-title}
```

### 5. GitHub CLI Integration with User Approval

**CRITICAL:** Always ask for user approval before creating PR:

1. **Generate PR Description**: Create the complete PR description
2. **Show Preview**: Display the PR description to user
3. **Request Approval**: Ask "Do you want to create this PR? (y/n)"
4. **If Approved**: Use `gh pr create` to create the PR
5. **If Declined**: Output description for manual PR creation

### 6. Issue Resolution Format

**Critical:** Use the correct GitHub keyword format for cross-repository issue closure:

```text
Closes 100x-fi/pensri-docs#{issue-number}
```

**Note:** This task will auto-close the issue in the pensri-docs repository when the PR is merged.

## Output Requirements

### 1. PR Description Output

Provide the complete PR description ready for GitHub:

```markdown
## Story Implementation

**Story:** 15.2 - Multi-Gateway Payment System Integration
**Story File:** [15.2.story.md](./docs/stories/15.2.story.md)

## Changes Made

### Summary

Implemented multi-gateway payment system integration allowing users to choose between Stripe and PayPal payment methods. Added payment method selection UI, gateway-specific processing logic, and comprehensive error handling.

### Key Changes

- Added payment gateway selection component
- Implemented Stripe and PayPal integration services
- Updated payment flow to support multiple gateways
- Added payment method validation and error handling

### Acceptance Criteria Met

- [x] User can select payment method (Stripe/PayPal)
- [x] Payment processing works for both gateways
- [x] Error handling for failed payments
- [x] Payment confirmation displays correct gateway info

## Testing

- [x] Unit tests added for payment services
- [x] Integration tests for both gateways
- [x] Manual testing with test cards/accounts
- [x] No regression in existing payment flow

## Files Changed

- `src/components/PaymentMethodSelector.tsx` (new)
- `src/services/paymentService.ts` (modified)
- `src/services/stripeService.ts` (new)
- `src/services/paypalService.ts` (new)
- `src/types/payment.ts` (modified)
- `tests/payment.test.ts` (modified)

## GitHub Issue

Closes 100x-fi/pensri-docs#173
```

### 2. GitHub CLI Command (if available)

```bash
# After user approval:
gh pr create \
  --title "Story 15.2: Multi-Gateway Payment System Integration" \
  --body "$(cat pr-description.md)" \
  --label "story,epic-15"
```

### 3. Manual Instructions (if GitHub CLI not available)

```text
1. Go to GitHub repository
2. Click "New Pull Request"
3. Set base branch to main/develop
4. Set compare branch to current branch
5. Copy the PR description above
6. Add appropriate labels
7. Create pull request
```

## Error Handling

**If story file not found:**

- HALT and inform user: "Story file {story-number}.story.md not found in 100x-fi/pensri-docs repository"
- Ask user to verify story number and check pensri-docs repository

**If GitHub Issue section missing:**

- WARN user: "No GitHub Issue section found in story file"
- Ask user to provide issue number manually
- Continue with PR creation using provided issue number

**If no changes detected:**

- WARN user: "No changes detected in current branch"
- Ask user to confirm they want to create PR anyway
- Suggest checking git status and commits

## Integration with Dev Agent Workflow

This task should be executed:

- After story implementation is complete
- Before marking story as "Ready for Review"
- When Dev Agent wants to create PR for code review

## Success Criteria

The task is successful when:

1. PR description is auto-populated from Dev Agent Record
2. GitHub issue in pensri-docs repository is linked and will auto-close
3. User approval is obtained before PR creation
4. All acceptance criteria and file changes are documented
5. Testing status is clearly indicated

## Key Principles

- Auto-populate from Dev Agent Record for accuracy
- Link to GitHub issues in pensri-docs repository with auto-close functionality
- Always request user approval before PR creation
- Include comprehensive change summary
- Document testing status clearly
- Follow project PR description conventions
- Make PR description self-contained and informative
