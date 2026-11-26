# Agentic AI – Day 2

## Overview

This notebook explores the development of LLM-powered business assistants using Python and the Groq API. It covers prompt design, chatbot development, customer message classification, structured data extraction, and conversation memory.

The practical implementations use **Sweet Crumbs Home Bakery** as a sample business and extend the concepts to a Fitness Studio assistant.

## Concepts Covered

- **LLM Integration:** Connecting language models using Groq API and LangChain.
- **Prompt Engineering:** Designing system prompts with business facts, rules, and response formats.
- **Prompt Injection Detection:** Exploring Llama Prompt Guard 2 to identify suspicious prompts.
- **Chatbot Development:** Building a business-specific conversational assistant.
- **Function Logging:** Using Python decorators to log function calls.
- **Conversation Memory:** Maintaining conversation history with a configurable context window.
- **Few-Shot Classification:** Classifying customer messages into order, question, or complaint.
- **Structured Output:** Extracting customer order details in JSON format.
- **Error Handling:** Handling API rate limits, connection errors, and JSON parsing errors.

## Practical Implementations

| Task | Implementation |
|---|---|
| Task 1 | Understanding the impact of removing chatbot rules from system prompts |
| Task 2 | Building a customer message classifier using few-shot examples |
| Task 3 | Extracting order details into structured JSON |
| Task 4 | Exploring conversation memory using a limited context window |
| Task 5 | Building a business-specific assistant for a Fitness Studio |

## Technologies Used

- Python
- Groq API
- LangChain
- GPT-OSS 120B
- GPT-OSS 20B
- Llama Prompt Guard 2
- OpenAI Python SDK
- JSON

## Setup and Execution

### 1. Install Dependencies

```bash
pip install langchain-groq groq openai
```

### 2. Configure API Key

Add your `GROQ_API_KEY` to Google Colab Secrets.

### 3. Run the Notebook

Open the notebook in Google Colab and execute the cells in sequence.

## Key Learning Outcomes

- Integrating LLMs into Python applications.
- Designing effective system prompts for business requirements.
- Building conversational assistants with context retention.
- Classifying user messages through few-shot prompting.
- Extracting structured information from natural language.
- Handling API errors and invalid model responses.
- Adapting chatbot functionality to different business domains.
