# Tool-calling Tutorial

## Introduction
This folder contains the step by step instructions on how to finetune a tool-calling using the distil labs CLI.


## Folder layout

```
├─ data/                    # Job description, train, test & config
├─ README.md                # (This file)
└─ model/                   # Populated after distil‑labs training download
```

## Understanding the data


### Train/test
The data consists of input/output pairs where the input is a question asked by a user about their finances and the output is a function call consisting of: the function to call + the parameters to pass to it.

For example:

```
Input:
How much did I spend on pets in September 2024?

Output:
{"name": "sum_transactions", "parameters": {"category": "pets", "start_date": "2024-09-01", "end_date": "2024-09-30"}}

```


### Job description
The job description consists of two main components:
- task_description: The high-level task we are aiming to solve
- tools: A full list of functions that can be called along with the parameters they take.

Below is the job description we use for this use-case. Take some time reviewing the specifics of how we structure the `tools` section. If you want to adapt this for your own use-case, you will need to carefully construct a full list of tools:

```json
{
  "task_description": "Respond with the next tool call to analyze expenses",
  "tools": [
    {
        "type": "function",
        "function": {
            "name": "count_transactions",
            "description": "Count the number of transactions matching the criteria. Can filter by category, date range, and amount limit.",
            "parameters": {
                "type": "object",
                "properties": {
                    "category": {
                        "type": "string",
                        "description": "The category to filter by (e.g., 'groceries', 'salary', 'entertainment'). If not provided, counts all categories."
                    },
                    "start_date": {
                        "type": "string",
                        "description": "Start date in YYYY-MM-DD format. If not provided, uses earliest date in data."
                    },
                    "end_date": {
                        "type": "string",
                        "description": "End date in YYYY-MM-DD format. If not provided, uses latest date in data."
                    },
                    "min_amount": {
                        "type": "number",
                        "description": "Optional minimum amount limit. Only count transactions with absolute value greater than or equal to this."
                    },
                    "max_amount": {
                        "type": "number",
                        "description": "Optional maximum amount limit. Only count transactions with absolute value less than or equal to this."
                    }
                },
                "required": []
            }
        }
    },
    {
        "type": "function",
        "function": {
            "name": "sum_transactions",
            "description": "Sum the total amount of transactions matching the criteria. Returns negative for expenses, positive for income (like salary). Can filter by category, date range, and amount limit.",
            "parameters": {
                "type": "object",
                "properties": {
                    "category": {
                        "type": "string",
                        "description": "The category to filter by (e.g., 'groceries', 'salary', 'entertainment'). If not provided, sums all categories."
                    },
                    "start_date": {
                        "type": "string",
                        "description": "Start date in YYYY-MM-DD format. If not provided, uses earliest date in data."
                    },
                    "end_date": {
                        "type": "string",
                        "description": "End date in YYYY-MM-DD format. If not provided, uses latest date in data."
                    },
                    "min_amount": {
                        "type": "number",
                        "description": "Optional minimum amount limit. Only count transactions with absolute value greater than or equal to this."
                    },
                    "max_amount": {
                        "type": "number",
                        "description": "Optional maximum amount limit. Only sum transactions with absolute value less than or equal to this."
                    }
                },
                "required": []
            }
        }
    },
    {
        "type": "function",
        "function": {
            "name": "compare_periods",
            "description": "Compare total spending or income between two time periods. Returns the sum for each period and the difference. Useful for questions like 'did I spend more in Q1 or Q2?'",
            "parameters": {
                "type": "object",
                "properties": {
                    "period1_start": {
                        "type": "string",
                        "description": "Start date of first period in YYYY-MM-DD format"
                    },
                    "period1_end": {
                        "type": "string",
                        "description": "End date of first period in YYYY-MM-DD format"
                    },
                    "period2_start": {
                        "type": "string",
                        "description": "Start date of second period in YYYY-MM-DD format"
                    },
                    "period2_end": {
                        "type": "string",
                        "description": "End date of second period in YYYY-MM-DD format"
                    },
                    "category": {
                        "type": "string",
                        "description": "Optional category to filter by. If not provided, compares all transactions."
                    }
                },
                "required": ["period1_start", "period1_end", "period2_start", "period2_end"]
            }
        }
    },
    {
        "type": "function",
        "function": {
            "name": "average_monthly_expenses",
            "description": "Calculate the average monthly expenses over a time period. Only includes expenses (negative amounts), not income. Can optionally filter by category.",
            "parameters": {
                "type": "object",
                "properties": {
                    "start_date": {
                        "type": "string",
                        "description": "Start date in YYYY-MM-DD format"
                    },
                    "end_date": {
                        "type": "string",
                        "description": "End date in YYYY-MM-DD format"
                    },
                    "category": {
                        "type": "string",
                        "description": "Optional category to filter by (e.g., 'groceries', 'entertainment'). If not provided, includes all expense categories."
                    }
                },
                "required": ["start_date", "end_date"]
            }
        }
    }
 ]
}
```


###  Task type
Tool calling trains a model to select and invoke the appropriate function or API based solely on the user’s request, without requiring additional context. The model learns to map natural language queries to structured tool calls with correct parameters, relying on its training rather than retrieved documentation.

This task type is ideal when you need a model that can reliably dispatch user intents to specific backend functions, APIs, or services in a deterministic, schema-compliant way.

### Config
The config file allows us to have fine-grained control over the pipeline. It allows us to control aspects of the pipeline relating to the tuning, synthetic data generation and evaluation. This is where we can define which teacher models to use, which student model to finetune and a host of other options. When we iterate on our development and try to improve upon our model, we typically make changs to the config and the job description whilst the other inputs remain static.



## Installation

Run the following command to install the distil labs CLI:

```
curl -fsSL https://cli-assets.distillabs.ai/install.sh | sh
```

To ensure everything is installed correctly, run the command:

```
distil
```

And you should see the available commands.

If you haven't already registered, you can do so using the command:

```
distil register
```

If you already have an account, you can enter your username and password when running the command:

```
distil login
```

To verify you have successfully logged in, run:

```
distil whoami
```


## Create model and run pipeline using CLI

### Create a model
Run the following command to create a new model:

```
distil model create my-first-model
```

### Upload data
To upload data, run the following command:
```
distil model upload-data <MODEL_ID> --data /Users/user/Documents/tool-calling-tutorial/data
```

(Note that this is the directory that contains: `train.jsonl`, `test.jsonl`, `config.yaml`, `job_description.jsonl`, `unstructured.jsonl` (optional))


To run the teacher evaluation we use the command:

```
distil model run-teacher-evaluation <MODEL_ID>
```

This will take a few minutes to complete, after which you can check the results using the command:

```
distil model teacher-evaluation <MODEL_ID
```

If you are satisfied with the performance, we can proceed to running the full distillation pipeline.

### Run training

To run the full distillation pipeline, run:
```
distil model run-training <MODEL_ID>
```

This process can take 6+ hours to run so you can periodically check the status of the training using the command:

```
distil model training <MODEL_ID>
```

When the training is complete, you can the following command to get the results:

```
distil models show <MODEL_ID>
```

And you can use the following command to download your model and deploy it using the inference framework of your choice (i.e. vLLM, Ollama):

```
distil models download <MODEL_ID>
```