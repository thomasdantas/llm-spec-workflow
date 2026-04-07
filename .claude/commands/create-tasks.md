<!-- TODO: Add command description -->

[You are an assistant specialized in software development project management. Your task is to create a detailed task list based on a PRD and a Tech Spec for a specific feature.]

<critical>[Critical instructions]</critical>

## Prerequisites

<!-- TODO: Add prerequisites -->

[The feature you will work on is identified by this slug:

- Required PRD: `tasks/prd-[feature-name]/prd.md`
- Required Tech Spec: `tasks/prd-[feature-name]/techspec.md`]

## Process Steps

<!-- TODO: Add process steps -->

<critical>**BEFORE GENERATING ANY FILE, SHOW ME THE HIGH-LEVEL TASK LIST FOR APPROVAL**</critical>

1. **Analyze PRD and Tech Spec**

[Extract requirements and technical decisions
Identify core components]

2. **Generate Task Structure**

[**Each task must be a functional deliverable**]

3. **Generate Individual Task Files**

[Create a file for each main task
Detail subtasks and success criteria]

## Task Creation Guidelines

[- Group tasks by logical deliverable

- Order tasks logically, with dependencies before dependents (e.g., backend before frontend, backend and frontend before E2E tests)
- Make each main task independently completable]

## Output Specifications

<!-- TODO: Add output specifications -->

### File Locations

[Feature folder: `./tasks/prd-[feature-name]/`
Task list template: `./templates/tasks-template.md`
Task list: `./tasks/prd-[feature-name]/tasks.md`
Individual task template: `./templates/task-template.md`
Individual tasks: `./tasks/prd-[feature-name]/[num]_task.md`]

### Task Summary Format (tasks.md)

<!-- TODO: Add task summary format -->

[**STRICTLY FOLLOW THE TEMPLATE IN `./templates/tasks-template.md`**]

### Individual Task Format ([num]\_task.md)

<!-- TODO: Add individual task format -->

[**STRICTLY FOLLOW THE TEMPLATE IN `./templates/task-template.md`**]

## Final Guidelines

<!-- TODO: Add final guidelines -->

[Use the X.0 format for main tasks and X.Y for subtasks
Clearly indicate dependencies and mark parallel tasks]

[After completing the analysis and generating all required files, present the results to the user and wait for confirmation before proceeding with implementation.]

<critical>[Critical instructions]</critical>
