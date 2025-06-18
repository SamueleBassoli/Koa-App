Koa - Development Roadmap
This document serves as the development checklist and reference for all tasks managed by the AI agent (Cursor).

Phase 2: Project Scaffolding & Foundations
[x] Initialize React Native project.

[x] Link project to the GitHub repository.

[x] Perform initial boot and verify app runs on the emulator.

[ ] Task 4: Implement navigation structure with React Navigation.

[ ] Install necessary dependencies.

[ ] Create a Bottom Tab Bar with 5 tabs: Home, Reports, Coach, Cookbook, Settings.

[ ] Create placeholder screen files in /src/screens.

[ ] Link each screen component to its corresponding tab.

Phase 3: UI Implementation
[ ] Task 1: Implement the Settings screen UI.

[ ] Build the visual layout based on the Figma design.

[ ] Utilize react-native-paper components.

[ ] Task 2: Implement the Dashboard (Home) screen UI.

[ ] Task 3: Implement the Reports screen UI.

[ ] Task 4: Implement the Cookbook screen UI.

[ ] Task 5: Implement the Coach (Chat) screen UI.

Phase 4: Business Logic & Data Layer
[ ] Task 1: Create StorageService.js for local storage management with AsyncStorage.

[ ] Task 2: Create ToolService.js and implement saveRecipe and createTask functions.

[ ] Task 3: Create GeminiService.js for Gemini API integration.

[ ] Implement function calling logic.

[ ] Task 4: Connect business logic to the Chat screen.

[ ] Handle user message submission.

[ ] Handle AI response rendering.

[ ] Trigger "Tools" when requested by the AI.

Phase 5: Polishing & Refinement
[ ] Implement loading indicators ("spinners") in the chat interface.

[ ] Implement connection error handling and user feedback.

[ ] Create a brief onboarding flow for first-time users.