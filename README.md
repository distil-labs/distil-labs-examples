# distil labs examples

Welcome to the distil labs platform - your gateway to effortless model fine-tuning without extensive machine learning expertise.

## Overview

The distil labs platform is a user-friendly solution that democratises access to state-of-the-art model fine-tuning. Whether you're a developer, researcher, or business professional, you can create custom, high-performance models tailored to your specific needs overnight.


## Examples

This repository contains practical examples demonstrating various use cases of the distil labs platform. Each example is contained in its own directory with complete code and documentation.

### Text classification: training and deployment
[This example](classification-tutorial) demonstrates how to fine-tune a small language model (SLM) for text classification and deploy it on your local machine. You can train a model that solves any of the four example tasks we provide or modify any of the examples to match your use-case. 


### Question Answering: training and deployment for open book QA
[This example](question-answering-tutorial) demonstrates how to fine-tune a small language model (SLM) for open-book question answering. In the Open-book QA setting, the LLM can refer to external sources of information (e.g., contexts gathered by the retriever) to answer given questions. You can train and deploy a model that solves QA task we provide or modify it to match your use-case.


### Text classification: how to write a job description
In [this example](rag-tutorial), start with a baseline RAG prototype for Roman‑Empire question answering, then fine‑tune an SLM with distil labs and run the entire system locally.


## Getting Started


To start working with this repository:
1. Clone this repository (or download as a zip file)
2. Make sure you have python 3.10 or later installed on your machine
3. Open the terminal and navigate to the direcotory of this README
4. Create a [python virtual environment](https://docs.python.org/3/library/venv.html#) using `python3 -m venv .distilenv`
5. Activate the environment with one of the folloing commands:

| Platform | Shell | Command to activate virtual environment |
| --- | --- |----------------------------------------|
| POSIX | bash/zsh | `$ source .distilenv/bin/activate`      |
|  | fish | `$ source .distilenv/bin/activate.fish` |
|  | csh/tcsh | `$ source .distilenv/bin/activate.csh`  |
|  | pwsh | `$ .distilenv/bin/Activate.ps1`         |
| Windows | cmd.exe | `C:\> .distilenv\Scripts\activate.bat`  |
|  | PowerShell | `PS C:\> .distilenv\Scripts\Activate.ps1` |

6. Install jupyter with `pip install jupyter`
7. Launch jupyter in your browser with `jupyter notebook`
8. Navigate to any of the examples using the browser

## Contributing

We welcome contributions! Please submit a PR if you want to contribute a new example.

## Documentation

Visit [distil labs](https://distillabs.ai) to learn more about our platform and our [documentation](https://docs.distillabs.ai) for details on our endpoints.
