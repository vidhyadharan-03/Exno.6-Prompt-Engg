# Exno.6-Prompt-Engg

## Aim: 
Development of Python Code Compatible with Multiple AI Tools

## Algorithm: 
Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights.

## Objective:
Build a Python script that:

a. Connects to multiple AI services via APIs.

b. Sends standardized prompts or inputs.

c. Collects and stores the outputs.

d. Compares the outputs for quality, tone, performance, or accuracy.

e. Generates reports or logs for further analysis.

This process helps in benchmarking AI tools and determining the best tool for a particular task or use case.

## Procedure / Algorithm:
### Step 1: Define the Use Case
Choose a specific AI task where multiple tools can be compared, such as:

a. Text summarization

b. Image generation

c. Audio synthesis

d. Sentiment analysis

e. Translation

Example Use Case: Compare summarization capabilities of ChatGPT (OpenAI) and Cohere.

### Step 2: Set Up API Access
Register or subscribe to APIs of the tools you want to use.

Store API keys securely (e.g., using environment variables or secrets module).

```python
import os

OPENAI_API_KEY = os.getenv("OPENAI_API_KEY")
COHERE_API_KEY = os.getenv("COHERE_API_KEY")
```

### Step 3: Write API Interaction Functions
Create reusable functions to interact with each AI service.

```python

import openai
import cohere

def get_openai_summary(text):
    openai.api_key = OPENAI_API_KEY
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": f"Summarize this: {text}"}]
    )
    return response['choices'][0]['message']['content']

def get_cohere_summary(text):
    co = cohere.Client(COHERE_API_KEY)
    response = co.summarize(text=text)
    return response.summary
```

### Step 4: Prepare a Prompt Dataset
Store a list of test inputs (e.g., articles or paragraphs) to run through both tools.

```python

test_inputs = [
    "Artificial intelligence (AI) is rapidly evolving and...",
    "Climate change is one of the most pressing issues..."
]
```

### Step 5: Compare Outputs Programmatically
Loop through inputs, collect summaries, and store them for analysis.

```python

results = []

for text in test_inputs:
    openai_output = get_openai_summary(text)
    cohere_output = get_cohere_summary(text)
    
    comparison = {
        "input": text,
        "openai_summary": openai_output,
        "cohere_summary": cohere_output
    }
    results.append(comparison)
```

### Step 6: Generate Actionable Insights
Apply analysis, such as:

a. Word count comparison

b. Sentiment scoring

c. Keyword extraction

d. Readability score

```python

from textblob import TextBlob

def analyze_summary(summary):
    blob = TextBlob(summary)
    return {
        "word_count": len(summary.split()),
        "sentiment": blob.sentiment.polarity,
        "readability": blob.sentiment.subjectivity
    }

for result in results:
    result["openai_analysis"] = analyze_summary(result["openai_summary"])
    result["cohere_analysis"] = analyze_summary(result["cohere_summary"])
```

### Step 7: Output a Summary Report
Export findings to JSON or CSV.

```python

import json

with open("summary_comparison.json", "w") as f:
    json.dump(results, f, indent=4)
```
Result:
The Python code successfully:

1. Connected with multiple AI tools using APIs.

2. Sent uniform prompts for consistent evaluation.

3. Collected and compared results using natural language metrics.

4. Generated structured, actionable insights that can be used to evaluate tool performance.

## Conclusion:
This experiment demonstrates how Python can serve as a powerful bridge between multiple AI tools, enabling developers to create multi-model pipelines that evaluate, compare, or combine the strengths of various services. This integration supports:

1. Better decision-making on tool selection

2. Automation of evaluation and benchmarking

3. Enhanced productivity by combining outputs

Such a system is scalable and can be adapted for broader use cases including multi-tool chatbots, creative content workflows, or research benchmarking.


## Result: 
The corresponding Prompt is executed successfully
