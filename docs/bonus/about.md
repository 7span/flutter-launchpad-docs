---
sidebar : 1
---

# GitHub Best Practices 🌳

Here are some tips and best practices to follow for GitHub.

### 1. Branching name conventions

branches name should be in lowercase and hyphen-separated.
Here are some examples :
- `feature/ticket-module` (for new features)
- `fix/bug-fixes` (for bug resolutions)
- `docs/update-doc` (for documentation updates)
- `refactor/auth-service-cleanup` (for code restructuring without changing external behavior)
- `hotfix/critical-data-issue` (for urgent fixes to production)

### 2. Commit message

**Writing style**: Write clear, concise, and descriptive commit messages. A good commit message explains what was changed and why.

**Reference Issues**: Link to relevant issues by including Fixes #ISSUE_NUMBER or Closes #ISSUE_NUMBER in your commit message to automatically close the issue when the PR is merged.

### 3. Descriptive Pull Request

A well-described PR makes the review process smoother and faster.

- Briefly **explain** what the PR does.
- Explain how you tested your changes and any relevant **test cases**.
- Crucially, for UI changes or complex features, include **screenshots**, **before-after images** or **short videos** directly in your PR description.
- If applicable, include a **checklist for reviewers** to ensure all necessary checks are performed.

### 4. Issue Creation and Management

Issues are central to tracking work, bugs, and feature requests.

- Use concise and descriptive titles and provide all necessary information.
- For bug reporting provide steps to reproduce, expected behavior, actual behavior, environment details (OS, browser, etc.), screenshots/videos if helpful.
- Use labels (e.g., bug, enhancement, documentation, help wanted, good first issue, priority: high, status: in progress) to categorize and organize issues.
- Assign issues to the person responsible for working on them.
- Group related issues into milestones to track progress towards a larger goal or release.
- Use issue templates to standardize the information requested for different types of issues (bugs, feature requests).

**Issue example**

```
### Current Problem
Manually creating the repository, BLoC, models, and screens for each feature that follows consistent structure is time-consuming, and error prone. Main goal is to eliminate this repetitive task by code-generation. 

### Solution
We will implement mason with brick configuration for adding new feature seamlessly with single command.

### Detailed Implementation : 
- Brick that generates module structure we follow in boilerplate having repository, bloc, screen and model folders.
- Repository will contain api integration for CRUD operation leveraging fp_dart.
- Model is pre-defined class that contains feature and pagination data.
- Bloc folder will have state class with handling pagination and api status. Event class will define events for fetching data with api and other CRUD operations which bloc will implement, including pagination to load more data.
- Screen will listen to bloc and will show Loading indicator , list of data , empty screen UI accordingly.
- Updating script to initialise mason_cli , mason and brick related configuration. 
- Documenting the steps about how to generate feature using mason.

# Folder Structure
lib  
└── module  
    ├── feature  
    │   ├── bloc  
    │   │   ├── feature_bloc.dart  
    │   │   ├── feature_event.dart  
    │   │   └── feature_state.dart  
    │   ├── model  
    │   │   └── feature_response_model.dart  
    │   ├── repository  
    │   │   └── feature_repository.dart  
    │   ├── screens  
    │   │   └── feature_screen.dart  
```                          

### 5. Bonus tips

1. Regularly Pull from Main/Develop
2. Keep Branches Small and Focused
3. Follow code review best practices
4. Use `.gitignore` to prevent unnecessary files from being committed
5. Do not provide too many files to review in single PR

These practices, when consistently applied, can significantly improve team collaboration, code quality, and project maintainability on GitHub.
