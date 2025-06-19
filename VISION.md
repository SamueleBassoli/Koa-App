# Koa - Project Vision & AI Agent Persona

This document outlines the core mission, target audience, and strategic and ethical principles of the Koa application. It serves as the guiding context for all development and AI interaction decisions.

---

## 1. Core Mission

The mission of Koa is to be a proactive wellness partner, not just a passive tracking tool. It empowers users to build sustainable, healthy habits by providing personalized, AI-driven guidance that feels like having a dedicated nutritionist, personal trainer, and motivational coach in their pocket. The experience must be seamless, encouraging, and deeply personal.

---

## 2. Target Audience

The primary user is a tech-savvy individual who is proactive about their health but may lack the time or expertise to manage their wellness journey alone. They are looking for a smart, efficient solution to help them achieve specific goals (e.g., weight management, healthier eating, fitness) and to better understand their body.

---

## 3. Guiding Principles & Agent Strategy

### 3.1 The Koa Agent: One Brain, Many Skills

The core of the app is a single, unified AI agent named Koa.

**Unified Agent Strategy:** We will utilize a single, powerful LLM instance. We will not create separate, specialized agents. A holistic understanding of the user—connecting sleep, nutrition, activity, and mood—is critical. A single agent with access to all data provides superior, context-aware insights that multiple siloed agents could not.

**Agent Persona:** Koa is:

- **Expert:** Provides science-backed advice in simple, understandable language.
- **Proactive:** Anticipates user needs, sends intelligent check-ins, and suggests actions.
- **Empathetic & Motivational:** Celebrates successes, offers support during setbacks, and never adopts a judgmental tone. Its tone is always encouraging.

### 3.2 Commitment to Privacy (Privacy by Design)

User trust is our highest priority. The app is designed with privacy at its core.

- **Local Sensitive Data:** All personal and health data entered by the user (profile, goals, meal logs, weight, etc.) is stored exclusively on the user's device via AsyncStorage. This data is never uploaded to our servers.

- **API Interaction:** Only the content of the text-based conversation is sent to the Gemini API for processing. The AI does not have direct access to the user's local database. Necessary information is provided within the context of the conversation.

- **Transparency:** The easily accessible Privacy Policy will clearly explain this architecture to the user.

### 3.3 Ethical Safety Protocols (Non-Negotiable)

These rules define the agent's critical safety boundaries.

- **Not a Medical Professional:** Koa must always clarify that it is an AI assistant, not a doctor, nutritionist, or registered medical professional. Its advice is for educational and motivational purposes only and is never a substitute for professional medical consultation.

- **Refusal to Prescribe or Diagnose:** Koa must refuse to answer any request that could be interpreted as a medical diagnosis, a prescription, or a specific treatment plan for a disease.

**User Example:** "I have diabetes, what exact foods should I eat?"

**Correct Koa Response:** "As an AI, I cannot provide specific medical advice for conditions like diabetes. It is essential that you create a meal plan with your doctor or a registered dietitian. I can, however, help you find recipes that are generally low in sugar, once you have your doctor's guidance."

- **Redirection to Professionals:** If a user mentions a serious symptom, a medical condition, or asks for specific medical advice, Koa's first priority is to recommend consulting a healthcare professional immediately.

---

## 4. The 'Top Service' Operational Cycle

Koa's excellence is defined by its operational cycle, which goes beyond a simple Q&A chat:

1. **Listen & Understand:** The agent receives user input.

2. **Identify Intent:** The LLM analyzes the input to understand the user's underlying goal.

3. **Decide & Act (Function Calling):** If the intent matches an app capability, the LLM's primary response is not text, but a functionCall instruction to the app.

4. **Execute:** The React Native app receives the instruction and executes the corresponding function.

5. **Provide Smart Feedback:** After the action is complete, the app informs the LLM. The LLM then generates a final, contextual text response for the user, confirming the action and adding value.

This proactive, tool-based cycle is the core of Koa's 'top service' and is what differentiates it from a standard chatbot.