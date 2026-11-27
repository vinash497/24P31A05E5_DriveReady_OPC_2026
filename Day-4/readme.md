# Studio Kit Booking Assistant – AI Tool Calling with Groq and LangChain

## Project Overview

The Studio Kit Booking Assistant is an AI-powered business assistant designed to manage customer booking enquiries and studio equipment availability.

The system uses Groq as the LLM provider and LangChain for tool integration, structured information extraction and agent execution.

The main objective is to understand how AI agents interact with external tools, extract meaningful information from customer messages and maintain business records.

### Technologies Used

- Python
- Groq API
- LangChain
- Pydantic
- Pandas
- Excel

---

# Task 1: Convert Python Functions into LangChain Tools

### Objective
Convert two existing Python functions into LangChain tools using the `@tool` decorator.

### Implementation Description

For the Studio Kit Booking business, two functions are converted into tools:

1. **Check Equipment Status:** Checks whether the camera, tripod and microphone are working properly.
2. **Check Kit Availability:** Checks whether the studio kit is available at a particular requested time.

The `@tool` decorator makes these Python functions accessible to a LangChain agent.

Each tool is provided with a meaningful name and a clear docstring describing its functionality. The docstring helps the AI model understand the purpose of the tool and determine when it should be used.

### Expected Result

The tools successfully perform their respective operations and return information about equipment status and booking availability.

### Learning Outcome

Learned how to convert normal Python functions into AI-accessible tools and how tool names, descriptions and input parameters help an AI agent select appropriate tools.

---

# Task 2: Create a Pydantic Model and Extract Structured Information

### Objective
Create a Pydantic model representing a single business record and use `with_structured_output` to extract information from five unstructured customer messages.

### Implementation Description

In a Studio Kit Booking business, customers may send booking enquiries in natural language. These messages may contain incomplete information, informal language or different ways of expressing dates and timings.

To organize this information, a Pydantic model named `BookingRecord` is created.

The model defines the following fields:

| Field | Description |
|---|---|
| Customer Name | Name of the customer |
| Phone | Customer contact number |
| Booking Date | Requested booking date |
| Start Time | Requested booking time |
| Duration | Booking duration in minutes |
| Equipment | Required studio equipment |
| Status | Current enquiry status |

The Groq model is connected to the Pydantic schema using LangChain's `with_structured_output` functionality.

Five different customer messages are provided as input. The AI extracts the relevant information and returns it in a structured format.

Optional fields are used to handle missing information. Business defaults are applied separately for fields such as booking duration and enquiry status.

### Expected Result

Five unstructured customer messages are converted into structured booking records with consistent fields.

### Learning Outcome

Learned how to define structured data using Pydantic, extract information from natural language, handle missing values and validate the structure of AI-generated information.

---

# Task 3: Create a Business Sheet and a Logging Tool

### Objective
Create a spreadsheet for the business and develop a `log_booking` tool to save customer booking records.

### Implementation Description

An Excel spreadsheet named `studio_bookings.xlsx` is created to maintain customer booking enquiries.

The spreadsheet contains customer details, contact information, requested booking dates, timings, duration, equipment and booking status.

A LangChain tool named `log_booking` is developed to save booking information into the spreadsheet.

Whenever the tool is invoked with the required customer details, a new record is appended to the Excel sheet.

This provides a simple method of maintaining business records without manually entering every booking enquiry.

### Expected Result

The booking information is successfully stored in the Excel spreadsheet, and previously saved records remain available for future reference.

### Learning Outcome

Learned how to connect LangChain tools with external data storage, create business records and automate spreadsheet updates using Python.

---

# Task 4: Experiment with Tool Names and Descriptions

### Objective
Understand how tool names and descriptions influence an AI agent's ability to identify and select the correct tool.

### Implementation Description

In this experiment, the original availability-checking tool is renamed to `tool1`, and its docstring is changed to a vague description: "does stuff".

The modified tool is then provided to the AI agent, and the agent is asked whether the studio kit is available at a particular time.

The agent's tool-selection behaviour is observed.

After the experiment, the original tool name and descriptive docstring are restored.

### Observation

A meaningful tool name and clear description provide useful information to the AI model about the functionality of a tool.

When the tool name and description are vague, the model receives less guidance and may find it more difficult to identify the appropriate tool.

However, a vague description does not necessarily prevent the model from selecting the correct tool because it can also use the available input schema and context.

### Expected Result

The experiment demonstrates the importance of meaningful tool names and descriptive docstrings in improving tool-selection reliability.

### Learning Outcome

Understood how tool metadata influences AI agent behaviour and why tools should have clear, descriptive names and explanations.

---

# Task 5: Read and Analyse the Execution Trace Using pretty_print()

### Objective
Inspect the execution trace of an AI agent, identify the model and tool interactions, and count the number of model calls and tool calls.

### Implementation Description

The AI agent is provided with a question asking it to check the equipment status and studio kit availability.

The agent identifies the required tools and executes them to obtain the requested information.

The `pretty_print()` method is used to display the messages exchanged during agent execution.

The execution trace helps identify:

- The original user request.
- The AI model's tool-selection decisions.
- The tools invoked by the agent.
- The results returned by the tools.
- The final response generated by the model.

The number of model calls is counted by identifying AI messages, while tool calls are counted using the tool-call information contained in those messages.

### Expected Execution Flow

1. The user submits a booking-related question.
2. The Groq model analyses the request.
3. The model selects the required tools.
4. The selected tools execute and return their results.
5. The model processes the returned information.
6. The final response is generated.

### Expected Result

For an execution in which both tools are called in one round and the model generates one final response:

- Model calls: 2
- Tool calls: 2

Actual counts may vary depending on the agent's execution.

### Learning Outcome

Learned how to inspect agent execution, understand the interaction between models and tools, trace tool invocations and measure the number of model and tool calls.

---

# Overall Learning Outcomes

By completing these five tasks, the following concepts were understood:

1. **LangChain Tools:** Converting Python functions into tools that an AI agent can use.
2. **Pydantic:** Defining and validating structured business records.
3. **Structured Output:** Extracting meaningful information from unstructured customer messages using Groq.
4. **Data Storage:** Maintaining business records using Excel and Python.
5. **Tool Selection:** Understanding the importance of meaningful tool names and descriptions.
6. **Agent Execution:** Analysing the interaction between an AI model and external tools using execution traces.

# Conclusion

The Studio Kit Booking Assistant demonstrates how Groq and LangChain can be used to build a simple AI-powered business automation system.

Through these tasks, Python functions are converted into AI-accessible tools, customer enquiries are transformed into structured records, business information is stored in an Excel sheet, and agent execution is analysed.

This practical implementation provides an understanding of the fundamental concepts involved in developing tool-using AI agents and applying them to real-world business scenarios.
