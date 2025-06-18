# Koa - Development Roadmap

This document serves as the detailed, step-by-step development checklist and reference for all tasks managed by the AI agent (Cursor). We will tackle one task at a time to ensure stability and correctness.

---

## Phase 2: Project Scaffolding & Foundations

- [x] Initialize React Native project.
- [x] Link project to the GitHub repository.
- [x] Perform initial boot and verify app runs on the emulator.

### Task 4: Implement navigation structure with React Navigation

- [ ] Install dependencies: @react-navigation/native, @react-navigation/bottom-tabs, react-native-screens, react-native-safe-area-context.
- [ ] Create a new directory: /src/navigation.
- [ ] Inside /src/navigation, create the main navigator file: AppNavigator.js.
- [ ] In App.tsx, import and render the AppNavigator.
- [ ] In AppNavigator.js, set up a NavigationContainer.
- [ ] Inside the container, create a BottomTabNavigator with 5 tabs: Home, Reports, Coach, Cookbook, Settings.
- [ ] For each tab, create a placeholder screen file in /src/screens (e.g., HomeScreen.js, ReportsScreen.js, etc.). Each screen should just display its name for now.
- [ ] Link each screen component to its corresponding tab in the BottomTabNavigator, assigning an appropriate icon from react-native-paper/icons to each.

---

## Phase 3: UI Implementation

### Task 1: Implement the Settings screen UI

- [ ] Open /src/screens/SettingsScreen.js.
- [ ] Build the static layout using View, Text, and ScrollView from React Native, and List.Section, List.Item from react-native-paper.
- [ ] Style the components to precisely match the Figma design.

### Task 2: Implement the Dashboard (Home) screen UI

- [ ] Open /src/screens/HomeScreen.js.
- [ ] Build the layout with sections for "Today's Progress", "Activity", and "Meals".
- [ ] Use Card and ProgressBar components from react-native-paper.
- [ ] Style all elements to match Figma.

### Task 3: Implement the Reports screen UI

- [ ] Open /src/screens/ReportsScreen.js.
- [ ] Build the layout with sections for Weight, Activity, Sleep, and Nutrition. For now, use placeholder images or simple boxes where the graphs will go.

### Task 4: Implement the Cookbook screen UI

- [ ] Open /src/screens/CookbookScreen.js.
- [ ] Build a grid layout using FlatList to display recipe cards.
- [ ] Design a single RecipeCard component in /src/components/RecipeCard.js that will be used in the grid.

### Task 5: Implement the Coach (Chat) screen UI

- [ ] Open /src/screens/CoachScreen.js.
- [ ] Build the chat layout using GiftedChat library or a custom FlatList solution.
- [ ] Design the message input bar with icons for camera and voice, using TextInput and IconButton from react-native-paper.

---

## Phase 4: Business Logic & Data Layer

### Task 1: Create StorageService.js

- [ ] Create the file in /src/services/.
- [ ] Implement saveData(key, value) function using AsyncStorage, including JSON.stringify and try...catch.
- [ ] Implement getData(key) function using AsyncStorage, including JSON.parse and try...catch.

### Task 2: Create ToolService.js

- [ ] Create the file in /src/services/.
- [ ] Import StorageService.
- [ ] Implement saveRecipe(recipeData) function. It should call saveData to store the recipe.
- [ ] Implement createTask(taskData) function. It should call saveData to store the task.

### Task 3: Create GeminiService.js

- [ ] Create the file in /src/services/.
- [ ] Define the schema for the tools (saveRecipe, createTask) that Gemini can call.
- [ ] Implement the main getAgentResponse(chatHistory) function that makes a fetch call to the Gemini API.
- [ ] Add logic to handle a standard text response.
- [ ] Add logic to handle a functionCall response from the API.
- [ ] Implement robust error handling for the API call.

### Task 4: Connect logic to the Chat screen

- [ ] In CoachScreen.js, manage the conversation state using useState.
- [ ] On message send, call getAgentResponse from GeminiService.
- [ ] Update the chat state with the AI's text response.
- [ ] If the AI requests a tool, call the appropriate function from ToolService and then send the result back to Gemini for a final summary message.

---

## Phase 5: Polishing & Refinement

### Task 1: Implement Loading Indicators

- [ ] In CoachScreen.js, show a "typing indicator" while waiting for the AI's response.
- [ ] In CookbookScreen.js and ReportsScreen.js, show a ActivityIndicator while data is being loaded from storage.

### Task 2: Implement Error Handling Feedback

- [ ] When an API call in GeminiService fails, show a Snackbar from react-native-paper to the user with a friendly error message (e.g., "Could not connect to Koa").

### Task 3: Create the Onboarding Flow

- [ ] Create a separate navigation stack for the onboarding screens (Profile, Goals, Allergies).
- [ ] On first app launch, show this onboarding flow.
- [ ] Upon completion, save a flag in AsyncStorage and navigate the user to the main app (Bottom Tab Bar).