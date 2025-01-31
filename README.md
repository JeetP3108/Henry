# Henry AI Tutor - Langflow Workflow

## Overview
Henry is an AI tutor designed to assist students in solving problems step by step. It evaluates problem difficulty, classifies the subject, and provides structured guidance. Additionally, it validates student responses, detects mistakes, and offers hints to improve learning.

## Workflow Structure
Henry consists of two primary workflows:

1. **Problem Breakdown and Stepwise Solution**
2. **Student Response Evaluation and Feedback**

Each workflow interacts with **Llama3.1 8B** via **Ollama** and maintains chat history using **Astra DB Chat Memory**.

## Installation and Setup
### Prerequisites
- **Langflow** installed
- **Ollama** (Llama3.1 8B model running locally)
- **Astra DB** setup for chat memory storage
- **Docker** (optional for running Langflow in a container)

### Steps to Set Up
1. Clone this repository:
   ```sh
   git clone https://github.com/your-repo/henry-ai-tutor.git
   cd henry-ai-tutor
   ```
2. Install required dependencies:
   ```sh
   pip install langflow
   ```
3. Run Langflow:
   ```sh
   langflow
   ```
4. Load the **Henry Workflow** inside Langflow.
5. Ensure **Ollama** is running:
   ```sh
   ollama run llama3
   ```
6. Configure **Astra DB** with your credentials for chat memory storage.

## Workflow Details

### **1. Problem Breakdown and Stepwise Solution Workflow**
Responsible for:
- Classifying the problem type.
- Assessing its difficulty level.
- Providing a structured, step-by-step solution.

#### **Flowchart:**
```
ChatInput → Prompt → Ollama → ChatOutput
```

#### **Step-by-Step Execution:**
1. **Receive Problem Statement**: The **ChatInput** node takes the problem statement from the user.
2. **Generate Prompt**: The **Prompt** node structures the problem-solving approach:
   - Classifies the problem under Mathematics, Physics, Coding, or Logic.
   - Determines the difficulty level (Beginner, Intermediate, Advanced).
   - Generates a **stepwise solution** without immediately revealing the final answer.
3. **AI Processing via Ollama**: Uses **Llama3.1 8B** to generate structured guidance.
4. **Output Stepwise Solution**: The response is displayed via **ChatOutput**.

### **2. Student Response Evaluation and Feedback Workflow**
Responsible for evaluating student responses, detecting mistakes, and providing constructive feedback.

#### **Flowchart:**
```
ChatInput → ConversationMemory → Prompt → Ollama → ChatOutput
```

#### **Step-by-Step Execution:**
1. **Store Conversation History**: **Astra DB Chat Memory** maintains previous interactions.
2. **Generate Prompt for Evaluation**: The **Prompt** node instructs the AI to:
   - Compare the **student’s response** with the expected answer.
   - Identify **errors** (calculation, conceptual, formatting).
   - Provide **hints** instead of direct answers.
   - Encourage retrying before revealing the next step.
3. **AI Processing via Ollama**: Uses **Llama3.1 8B** to evaluate responses and generate feedback.
4. **Output Feedback**: The AI response is sent to **ChatOutput**.

## Memory and Data Handling
- **Astra DB Chat Memory** stores conversation history to track student progress.
- **Message History** retrieves stored messages for continuous learning experiences.
