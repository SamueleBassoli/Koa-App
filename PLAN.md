# Koa - Development Roadmap (Optimized MVP)

This document serves as the detailed, step-by-step development checklist for the optimized MVP of the Koa application.

## Phase 2: Project Scaffolding & Foundations

- [x] Initialize React Native project.
- [x] Link project to the GitHub repository.
- [x] Perform initial boot and verify app runs on the emulator.
- [ ] **Task 4:** Implement navigation structure with `React Navigation`.
  - [ ] Install dependencies: `@react-navigation/native`, `@react-navigation/bottom-tabs`, `react-native-screens`, `react-native-safe-area-context`.
  - [ ] Create a new directory: `/src/navigation`.
  - [ ] Inside `/src/navigation`, create the main navigator file: `AppNavigator.js`.
  - [ ] In `App.tsx`, import and render the `AppNavigator`.
  - [ ] In `AppNavigator.js`, set up a `NavigationContainer`.
  - [ ] Inside the container, create a `BottomTabNavigator` with 4 tabs: `Home`, `Coach`, `Cookbook`, `Settings`.
  - [ ] For each tab, create a placeholder screen file in `/src/screens` (e.g., `HomeScreen.js`, `CoachScreen.js`, etc.). Each screen should just display its name for now.
  - [ ] Link each screen component to its corresponding tab in the `BottomTabNavigator`, assigning an appropriate icon from `react-native-paper/icons` to each.
- [ ] **Task 5:** Implement the Onboarding Flow with Medical Disclaimer.
  - [ ] Create a separate stack navigator for the onboarding screens in `/src/navigation/OnboardingNavigator.js`.
  - [ ] In `AppNavigator.js`, create a root stack navigator that decides whether to show the `OnboardingNavigator` or the `BottomTabNavigator` based on a state variable (e.g., `isOnboardingCompleted`).
  - [ ] **Sub-task 5.1:** Create the `DisclaimerScreen.js`.
    - [ ] Build the UI with `Text` and a `Checkbox` from `react-native-paper`.
    - [ ] The "Continue" button should be disabled until the checkbox is checked.
  - [ ] **Sub-task 5.2:** Create the `ProfileSetupScreen.js`.
    - [ ] Build the UI with `TextInput` components for age, sex, weight, and height.
  - [ ] **Sub-task 5.3:** Create the `GoalsSetupScreen.js`.
    - [ ] Use `Checkbox.Item` from `react-native-paper` to allow multiple selections.
  - [ ] **Sub-task 5.4:** Create the `AllergiesSetupScreen.js`.
    - [ ] Use `Chip` components from `react-native-paper` for selectable tags.
  - [ ] **Sub-task 5.5:** Implement the state management for the onboarding flow.
    - [ ] Use a `useState` hook in the root navigator to hold all the collected user data.
    - [ ] Pass setter functions down to each onboarding screen to update the state.
  - [ ] **Sub-task 5.6:** Implement the completion logic.
    - [ ] On the final step, save all collected data to AsyncStorage.
    - [ ] Save a flag to AsyncStorage (e.g., `onboarding_completed: true`).
    - [ ] Update the state to switch from the onboarding stack to the main app stack.

## Phase 3: UI Implementation

- [ ] **Task 1:** Implement the `Settings` screen UI.
  - [ ] Build the static layout to match the Figma design using `react-native-paper` components like `List.Section` and `List.Item`.
- [ ] **Task 2:** Implement the `Cookbook` screen UI.
  - [ ] In `/src/screens/CookbookScreen.js`, create a `useState` with a dummy array of recipe objects to simulate data.
  - [ ] Build a grid layout using `FlatList` with `numColumns={2}`.
  - [ ] Create a reusable `RecipeCard.js` component in `/src/components/` that takes a recipe object as a prop and displays its image and title.
- [ ] **Task 3:** Implement the `Coach` (Chat) screen UI.
  - [ ] In `/src/screens/CoachScreen.js`, build the static layout.
  - [ ] Use a `FlatList` to render chat messages.
  - [ ] Create a `MessageBubble.js` component in `/src/components/` to style user and AI messages differently.
  - [ ] Build the message input bar at the bottom using `TextInput` and `IconButton` from `react-native-paper`.
- [ ] **Task 4:** Implement the `Home` (Dashboard) screen UI.
  - [ ] In `/src/screens/HomeScreen.js`, build the static layout with sections for "Today's Progress" and "Meals".
  - [ ] Use `Card` and `ProgressBar` components from `react-native-paper`.
  - [ ] **Integrate a Placeholder Chart:** Install `react-native-chart-kit` and add a `LineChart` component with static, dummy data where the weight chart should go.

## Phase 4: Business Logic & Data Layer

- [ ] **Task 1:** Create `StorageService.js`.
  - [ ] Create the file in `/src/services/`.
  - [ ] Implement `saveData(key, value)` function using AsyncStorage, including `JSON.stringify` and `try...catch`.
  - [ ] Implement `getData(key)` function using AsyncStorage, including `JSON.parse` and `try...catch`.
- [ ] **Task 2:** Create `ToolService.js`.
  - [ ] Create the file in `/src/services/`.
  - [ ] Import `StorageService`.
  - [ ] Implement `saveRecipe(recipeData)` function. It should call `saveData`.
  - [ ] Implement `createTask(taskData)` function. It should call `saveData`.
  - [ ] Implement `generatePlan(prompt)` function. For now, it can just return a hardcoded plan string.
- [ ] **Task 3:** Create `GeminiService.js`.
  - [ ] Create the file in `/src/services/`.
  - [ ] Define the JSON schema for the three tools (`saveRecipe`, `createTask`, `generatePlan`).
  - [ ] Implement the main `getAgentResponse(chatHistory)` function that makes a `fetch` call to the Gemini API.
  - [ ] Add logic to handle a standard text response.
  - [ ] Add logic to handle a `functionCall` response from the API.
  - [ ] Implement robust error handling for the API call, returning a structured error object.
- [ ] **Task 4:** Connect logic to the Chat screen.
  - [ ] **Sub-task 4.1:** In `CoachScreen.js`, manage the conversation as an array of messages in a `useState` hook.
  - [ ] **Sub-task 4.2:** When the user sends a message, add it to the message array and call `getAgentResponse` from `GeminiService`.
  - [ ] **Sub-task 4.3:** While waiting for the response, set a `loading` state to true.
  - [ ] **Sub-task 4.4:** When the response arrives, if it's a text response, add it to the message array.
  - [ ] **Sub-task 4.5:** If the response is a `functionCall`, call the corresponding function from `ToolService`. After the tool executes, send a new message to Gemini with the result to get the final summary, and then add that summary to the message array.
  - [ ] **Sub-task 4.6:** Implement the "Weekly Check-in" logic: if the user types a specific phrase, trigger a call to the `generatePlan` tool.

## Phase 5: Polishing & Refinement

- [ ] **Task 1:** Implement Loading Indicators.
  - [ ] In `CoachScreen.js`, when the `loading` state is true, render a "typing indicator" component.
- [ ] **Task 2:** Implement Error Handling Feedback.
  - [ ] In `CoachScreen.js`, if the `getAgentResponse` call returns an error, use a `Snackbar` from `react-native-paper` to show a user-friendly error message.