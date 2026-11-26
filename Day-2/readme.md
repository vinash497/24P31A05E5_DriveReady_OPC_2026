
# Agentic AI – Day 2

## Overview

This notebook focuses on building LLM-powered business assistants using Python, Groq API, and LangChain.

The implementations demonstrate how to design business-specific system prompts, integrate language models, detect prompt injection attempts, classify customer messages, extract structured order information, maintain conversation history, and develop assistants for different business domains.

Two business scenarios are explored:

- **Sweet Crumbs Home Bakery** – An AI customer support assistant.
- **Fitness Studio** – An AI front-desk assistant for fitness packages and membership queries.

## Technologies Used

- Python
- Groq API
- LangChain Groq
- OpenAI Python SDK
- GPT-OSS 120B
- GPT-OSS 20B
- Llama Prompt Guard 2
- JSON
- Google Colab

## 1. LLM Integration

Integrated large language models using the Groq API and LangChain.

**Implementation:**
- Installed and imported `langchain_groq`.
- Initialized the `ChatGroq` model.
- Configured the Groq API key using Google Colab Secrets.
- Used temperature settings to control response generation.

**Models explored:**
- `openai/gpt-oss-120b`
- `openai/gpt-oss-20b`

## 2. Sweet Crumbs – AI Customer Support Assistant

Developed a business-specific chatbot for Sweet Crumbs Home Bakery.

### Business Information

| Item | Price |
|---|---:|
| Plum Cake | ₹500 |
| Chocolate Cake | ₹650 |
| Cupcake | ₹80 |

### System Prompt Design

The assistant is configured with:

- **Role:** Friendly customer support assistant.
- **Business Facts:** Menu, prices, ordering requirements, and eggless options.
- **Rules:** Orders require 24 hours' notice. Delivery times must never be promised.
- **Fallback:** If information is unavailable, the assistant responds with "I'll check with the owner."
- **Response Format:** Friendly responses under 50 words, in English or Telugu based on the customer's language.

### Implemented Features

- Business-specific customer conversations.
- Menu and price information.
- Customer name and order context retention.
- Friendly responses in English and Telugu.
- Business rules and response constraints.

## 3. Prompt Injection Detection

Explored prompt injection detection using **Llama Prompt Guard 2**.

**Implementation:**
- Integrated the `meta-llama/llama-prompt-guard-2-22m` model through Groq.
- Submitted a suspicious prompt containing an instruction to ignore previous instructions.
- Examined the model's response to the potentially malicious input.

**Objective:** Understand prompt injection attempts and explore an additional security layer for LLM-based applications.

## 4. Function Logging Using Decorators

Implemented a Python decorator to log function execution.

**Function:** `log_call()`

**Features:**
- Uses `functools.wraps` to preserve function metadata.
- Wraps the original function.
- Captures function arguments and returned values.
- Prints execution details for monitoring.

**Example:** `get_price(item, qty)`

This function calculates the total price of a bakery item based on its quantity.

## 5. Conversation Memory

Implemented conversation history management for the bakery assistant.

**Key Components:**
- `history`: Stores system, user, and assistant messages.
- `MAX_TURNS`: Controls the number of recent conversation messages retained.
- `chat()`: Handles user messages and generates responses using conversation history.

**Memory Configuration:**

- Initial configuration: `MAX_TURNS = 8`
- Memory experiment: `MAX_TURNS = 2`

The implementation retains the system prompt and a limited number of recent messages when sending requests to the model.

## 6. API Error Handling

Implemented error handling for API-related failures.

**Errors Handled:**

- `RateLimitError`: Handles API rate-limit issues.
- `APIConnectionError`: Handles connection failures.
- `JSONDecodeError`: Handles invalid JSON responses.

Fallback messages are returned when the API is unavailable or a response cannot be processed.

## 7. Practical Tasks

### Task 1: Understanding the Importance of System Prompt Rules

Removed the RULES section from the bakery assistant's system prompt and tested the question:

`Can you deliver in 1 hour?`

**Objective:**
Understand how removing business constraints affects the chatbot's responses and why system prompt rules are important.

### Task 2: Few-Shot Customer Message Classification

Developed a customer message classifier using three examples.

**Classification Categories:**
- `order`
- `question`
- `complaint`

**Few-Shot Examples:**

| Customer Message | Expected Classification |
|---|---|
| I want to book 10 cupcakes for Saturday. | order |
| Are your cakes eggless? | question |
| My plum cake arrived crushed. | complaint |

The classifier was tested with five additional customer messages.

**Implementation Details:**
- Created a system prompt with three classification labels.
- Provided three user-assistant example pairs.
- Used the GPT-OSS 120B model.
- Configured temperature to `0.0` for consistent classification.
- Handled API rate-limit and connection errors.

### Task 3: Structured Order Extraction Using JSON

Implemented an order extraction system that converts natural-language customer messages into structured JSON data.

**Required JSON Fields:**

| Field | Data Type | Description |
|---|---|---|
| `name` | String / Null | Customer name |
| `item` | String / Null | Ordered item |
| `qty` | Number / Null | Quantity |
| `date` | String / Null | Requested date |
| `eggless` | Boolean | Whether an eggless order is requested |

**Implementation Details:**
- Designed a prompt requiring valid JSON output.
- Extracted order information from customer messages.
- Removed Markdown code fences when present.
- Used `json.loads()` to convert JSON text into a Python dictionary.
- Handled invalid JSON and API errors using exception handling.

### Task 4: Conversation Memory Experiment

Tested the effect of reducing conversation memory from eight messages to two.

**Experiment:**
1. Set `MAX_TURNS = 2`.
2. Started a new conversation.
3. Told the assistant the customer's name.
4. Continued the conversation for three turns.
5. Asked the assistant to recall the customer's name.

**Objective:**

Understand how limiting conversation history affects the assistant's ability to retain previously shared information.

### Task 5: Building a Fitness Studio Assistant

Rebuilt the business assistant for a different domain using Fitness Studio as the business scenario.

#### Fitness Studio Catalogue

| Package | Price |
|---|---:|
| Morning Yoga Pass | ₹1,500 |
| Strength Batch | ₹2,200 |
| Weekend Sound Bath | ₹600 |

#### Business Information and Rules

- Morning batches start at 6:30 AM.
- Mats are provided free.
- The assistant must not guarantee spot availability.
- The assistant must not promise exact class end times.
- For unavailable information, it responds with "I'll check with the studio manager."
- Responses must be under 50 words.
- The assistant matches the member's language.

#### Implemented Functions

**1. `log_call()`**

A decorator that logs function execution, arguments, and returned values.

**2. `get_package_total(package, sessions)`**

Calculates the total price for a given fitness package based on the number of sessions.

- Accepts package name and session count.
- Normalizes package names using lowercase and whitespace removal.
- Retrieves the package price from the catalogue.
- Returns the calculated total.
- Returns `None` when the package is not found.

**3. `chat(user_text)`**

Handles conversations with Fitness Studio members.

- Maintains conversation history.
- Retains the system prompt.
- Sends recent messages to the LLM.
- Generates context-aware responses.
- Handles API rate-limit and connection errors.

#### Conversation Configuration

- Model: `openai/gpt-oss-20b`
- Temperature: `0.3`
- Maximum retained conversation messages: `8`

**Objective:** Apply the same AI assistant architecture to a different business domain by changing the business catalogue, system prompt, rules, and pricing function.

## 8. Key Learning Outcomes

- Integrating LLMs into Python applications.
- Using Groq API and LangChain for model interaction.
- Designing system prompts with business-specific rules.
- Understanding prompt injection detection.
- Implementing function logging using Python decorators.
- Building few-shot classification systems.
- Extracting structured information using JSON.
- Managing conversation history with a configurable context window.
- Handling API and JSON parsing errors.
- Reusing an assistant architecture across different business domains.

## Execution

This notebook is designed to run in **Google Colab**.

### Install Dependencies

```bash
pip install langchain_groq groq openai
```

### Configure API Key

Add `GROQ_API_KEY` to the Google Colab Secrets section.

### Run

Open the notebook in Google Colab and execute the cells in sequence.

