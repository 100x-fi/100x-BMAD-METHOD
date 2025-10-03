<!-- Powered by BMAD™ Core -->

# test-design

Retrieve the current date and add "End-to-End Test Cases" section in story file following the story template.

## Inputs

```yaml
required:
  - story_id: "{epic}.{story}" # e.g., "1.3"
  - story_path: "{devStoryLocation}/{epic}.{story}.*.md" # Path from core-config.yaml
  - story_title: "{title}" # If missing, derive from story file H1
  - story_slug: "{slug}" # If missing, derive from title (lowercase, hyphenated)
```

## Dependencies

```yaml
data:
  - story-tmpl.yaml
  - test-scenario-template.md
```

## Process

### 1. Analyze Story Requirements

Break down each acceptance criterion into testable scenarios. For each AC:

- Identify the core functionality to test
- Determine data variations needed
- Consider error conditions
- Note edge cases

### 2. Create End-to-End Test Cases

**Reference:** Load `story-tmpl.yaml` and `test-scenario-template.md` for template

Retrieve the current date and add "End-to-End Test Cases" section in story file following the story template.
