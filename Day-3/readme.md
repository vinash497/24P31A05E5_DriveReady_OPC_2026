# 🌱 GreenNest – AI Agents

## 📌 Overview

GreenNest is an AI-powered indoor plant store customer support assistant developed as part of the Day 3 AI Agents learning program.

This project uses **Python, LangChain, and Groq API** to build an AI assistant that helps customers choose indoor plants, understand product prices, receive plant-care suggestions, and enquire about orders.

It demonstrates the practical implementation of Python functions, LLM-based applications, prompt engineering, response evaluation, and AI Agents with tools.

## 🎯 Objectives

- Understand the fundamentals of AI Agents.
- Build a business-specific AI assistant using LangChain.
- Design system prompts with business facts, rules, and response formats.
- Create a customer test dataset using CSV.
- Evaluate AI responses using automated testing.
- Improve system prompts and compare test results.
- Experiment with different model temperature settings.
- Implement Python functions as AI Agent tools.
- Understand the difference between Python code, LLM calls, and AI Agents.

## 🛠️ Technologies Used

- **Programming Language:** Python
- **Platform:** Google Colab
- **LLM Framework:** LangChain
- **LLM Provider:** Groq API
- **Model:** GPT-OSS-20B
- **Dataset:** CSV

## 🏪 Business Overview – GreenNest

GreenNest is an indoor plant store that sells different varieties of indoor plants and provides basic plant-care guidance to customers.

### 🌿 Product Catalogue

| Product | Price |
|---|---:|
| Snake Plant | ₹450 |
| Money Plant | ₹250 |
| Peace Lily | ₹550 |
| Areca Palm | ₹700 |
| ZZ Plant | ₹600 |
| Decorative Pot | Additional ₹100 |

### 📋 Business Rules

- Every plant includes a basic care instruction card.
- Orders require at least 12 hours' notice.
- Delivery is available only within the business service area.
- Product availability must be checked before confirming an order.
- Customers can purchase decorative pots for an additional ₹100.
- The assistant must not invent product prices or business information.
- Unknown delivery information must be referred to the delivery team.

---

## 📚 Assignments and Implementation

### 1️⃣ Assignment 1 – Business Selection and System Prompt

Selected GreenNest as the business for developing an AI customer support assistant.

Created a system prompt containing the following components:

- **Role:** Defines the assistant's responsibilities.
- **Business Facts:** Contains product names, prices, and ordering information.
- **Business Rules:** Defines the conditions and limitations the assistant must follow.
- **Response Format:** Specifies the tone, response length, and communication style.

The system prompt helps the assistant provide consistent and business-specific responses.

### 2️⃣ Assignment 2 – Customer Test Dataset and Evaluation

Created a `tests.csv` dataset containing 10 realistic customer questions.

The dataset includes two columns:

- `question` – Contains customer queries.
- `must_include` – Contains the expected keyword in the assistant's response.

Implemented a Python `run_tests()` function using `csv.DictReader` to:

1. Read customer questions from the CSV file.
2. Send each question to the LangChain chain.
3. Compare the generated response with the expected keyword.
4. Display PASS or FAIL for each test.
5. Calculate the overall test pass rate.

#### 📊 Initial Test Results

| Metric | Result |
|---|---:|
| Total Tests | 10 |
| Passed | 9 |
| Failed | 1 |
| Pass Rate | 90% |

**Observation:**

The failed test involved an order delivery time question. The assistant provided the correct 12-hour notice information, but the keyword comparison did not match because of a whitespace-character difference.

### 3️⃣ Assignment 3 – System Prompt Improvement

Created an improved system prompt named `SYSTEM_V2`.

Added an additional instruction requiring the assistant to mention the exact numeric product price whenever answering price-related questions.

**Improvement:**

- Ensures exact numeric prices are included in responses.
- Improves consistency in product-price answers.
- Makes the system prompt more specific and clear.

This experiment demonstrates how modifying system prompt instructions can improve response consistency.

### 4️⃣ Assignment 4 – Temperature Experiment

Experimented with the Groq model's temperature setting.

- **Initial Temperature:** `0.3`
- **Modified Temperature:** `1.0`

Observed how temperature affects response generation and variability.

**Observations:**

- Lower temperature generally produces more consistent responses.
- Higher temperature allows greater variation in response generation.
- Different executions may produce different wording.
- Higher temperature does not necessarily improve response accuracy.

This experiment helps understand the relationship between model temperature and response variability.

### 5️⃣ Assignment 5 – Classification of Business Operations

Identified three business operations and classified them based on their implementation requirements.

#### 5.1 Plain Python Code – Price Calculation

Implemented a Python function to calculate the total price of plants and decorative pots.

**Implementation:**

```python
def calculate_total(price, quantity, pot=False):
    total = price * quantity

    if pot:
        total += 100

    return total

print(calculate_total(250, 2, True))
```

**Output:**

```text
600
```

The function performs mathematical calculations using predefined product prices without requiring an LLM.

#### 5.2 One LLM Call – Plant Recommendation

Used the Groq LLM to recommend indoor plants based on customer requirements.

**Example Customer Query:**

"My room receives very little sunlight. Suggest a suitable indoor plant."

The LLM understands the customer's requirements and generates a suitable plant recommendation.

This demonstrates how a single LLM call can understand natural-language input and generate useful responses without external tools.

#### 5.3 AI Agent – Complete Plant Order

Implemented an AI Agent using LangChain's `create_agent()` function.

Created two Python tools:

**1. `check_stock()`**

- Checks the availability of a particular plant.
- Uses predefined stock information.
- Returns the available quantity.

**2. `calculate_price()`**

- Calculates the total order price.
- Considers plant quantity.
- Includes decorative pot charges when applicable.

Integrated both tools with the AI Agent to handle a multi-step customer request.

**Example Customer Request:**

"I want 2 Peace Lilies with 2 decorative pots. Check availability and calculate the total price."

**Execution Result:**

- Peace Lily stock available: 5 units.
- Requested quantity: 2.
- Plant cost: ₹1,100.
- Decorative pot cost: ₹200.
- Total order price: ₹1,300.

The agent checked stock, calculated the total price, and generated a response without claiming that the order was confirmed.

---

## 🧠 Key Concepts Learned

- Difference between chatbots and AI Agents.
- Components of an AI Agent.
- Think–Act–Observe–Repeat agent loop.
- Traditional AI, Generative AI, and Agentic AI.
- LangChain models, prompt templates, and chains.
- System prompt design and prompt engineering.
- CSV-based automated response evaluation.
- Prompt improvement and testing.
- Model temperature and response variability.
- Python functions as AI Agent tools.
- Tool integration using LangChain agents.
- Practical implementation of business-specific AI assistants.

## 🚀 Conclusion

This project provided practical experience in developing an AI-powered business assistant using Python, LangChain, and Groq.

It demonstrated how traditional Python functions, LLM-based responses, and AI Agents can work together to solve different business problems.

GreenNest serves as a practical example of applying AI Agent concepts to customer support, plant recommendations, product information, and business operations.


