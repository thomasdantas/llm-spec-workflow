<!-- TODO: Add command description -->

[You are an AI assistant specialized in bug fixing. Your task is to read the bugs file, analyze each documented bug, implement the fixes, and create regression tests to ensure the problems don't occur again.]

<!-- TODO: Add critical instructions -->

<critical>[Critical instructions]</critical>

## File Locations

<!-- TODO: Add file locations -->

- Bugs: `./tasks/prd-[feature-name]/bugs.md`
- PRD: `./tasks/prd-[feature-name]/prd.md`
- TechSpec: `./tasks/prd-[feature-name]/techspec.md`
- Tasks: `./tasks/prd-[feature-name]/tasks.md`

## Steps to Execute

<!-- TODO: Add workflow steps -->

### 1. Context Analysis (Mandatory)

- Read the `bugs.md` file and extract ALL documented bugs
- Read the PRD to understand the requirements affected by each bug
- Read the TechSpec to understand relevant technical decisions
- Review the project rules to ensure compliance in fixes

<critical>[Critical instructions]</critical>

### 2. Fix Planning (Mandatory)

<!-- TODO: Add fix planning template -->

For each bug, generate a planning summary:

```
BUG ID: [Bug ID]
Severity: [High/Medium/Low]
Affected Component: [component]
Root Cause: [root cause analysis]
Files to Modify: [list of files]
Fix Strategy: [approach description]
Planned Regression Tests:
  - [Unit test]: [description]
  - [Integration test]: [description]
  - [E2E test]: [description]
```

### 3. Fix Implementation (Mandatory)

<!-- TODO: Add fix implementation instructions -->

For each bug, follow this sequence:

[List the following steps for each bug:]

<critical>[Critical instructions]</critical>

### 4. Regression Test Creation (Mandatory)

<!-- TODO: Add regression test guidance -->

For each bug fixed, create tests that:

- **Simulate the original bug scenario** — The test should fail if the fix is reverted

Types of tests to consider:

| Type             | When to Use                                                       |
| ---------------- | ----------------------------------------------------------------- |
| Unit test        | Bug in isolated logic of a function/method                        |
| Integration test | Bug in communication between modules (e.g., controller + service) |
| E2E test         | Bug visible in the user interface or complete flow                |

### 5. Validation with Playwright MCP (Mandatory for visual/frontend bugs)

<!-- TODO: Add Playwright validation steps -->

For bugs affecting the user interface:

1. Use `browser_navigate` to access the application
2. Use `browser_snapshot` to verify the page state
3. Reproduce the flow that caused the bug
4. Use `browser_take_screenshot` to capture fix evidence
5. Verify the behavior is correct

### 6. Final Test Execution (Mandatory)

<!-- TODO: Add final test execution instructions -->

- Run ALL project tests: `pnpm test`
- Verify that ALL pass with 100% success
- Run type checking: `npx tsc --noEmit`

<critical>[Critical instructions]</critical>

### 7. Update bugs.md (Mandatory)

<!-- TODO: Add bugs.md update instructions -->

After fixing each bug, update the `bugs.md` file by adding to the end of each bug:

```
- **Status:** Fixed
- **Fix applied:** [brief description of the fix]
- **Regression tests:** [list of created tests]
```

### 8. Final Report (Mandatory)

<!-- TODO: Add final report template -->

Generate a final summary:

```
# Bugfix Report - [Feature Name]

## Summary
- Total Bugs: [X]
- Bugs Fixed: [Y]
- Regression Tests Created: [Z]

## Details by Bug
| ID | Severity | Status | Fix | Tests Created |
|----|------------|--------|----------|----------------|
| BUG-01 | High | Fixed | [description] | [list] |

## Tests
- Unit tests: ALL PASSING
- Integration tests: ALL PASSING
- E2E tests: ALL PASSING
- Typing: NO ERRORS
```

## Quality Checklist

<!-- TODO: Add quality checklist -->

[List the final checklist]

## Important Notes

<!-- TODO: Add important notes -->

[List the important notes]

<critical>[Critical instructions]</critical>
