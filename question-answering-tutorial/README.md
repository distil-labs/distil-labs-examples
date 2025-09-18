# Fine-tune a small language model for open book question-answering

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/distil-labs/distil-labs-examples/blob/main/question-answering-tutorial/question-answering.ipynb)

The **distil labs** platform allows anyone to benefit from state-of-the-art methods for model fine-tuning. You don’t need to be a machine learning expert to get a highly performant model customized to your needs in a matter of a day. 


## End-to-end workflow
We will solve the question-answering task by going through the following process

1. **Task Definition**: We begin by defining our specific task by providing a small train/test dataset and the corresponding task description.
2. **SLM Training**: In this stage, we will validate if a large language model (LLM) can accurately solve our task, and if that is the case, we use all available data (both labelled and unlabelled) to train a specialized SLM to match the performance of the LLM.
3. **SLM Deployment**: Finally, we will receive our trained SLM binaries, and we can integrate them into our production environment. Note that deployment will be covered in the next notebook.
4. **SLM Retraining**: After deploying the first model, we can improve the performance of the initial model by providing additional training examples or by providing unlabeled contextual data. Note that we will not focus on retraining in this tutorial.


### Task Definition
You can use any of the four example problems to train your own model. Feel free to modify the example tasks to match your use-case os simply use them as they are! 

Each example dirctory outlined below contains the 4 main components of a task:
1. **Job description** that explains the question-answering task and describes all classes
2. **Train dataset** (~10s examples) which demonstrates our expected inputs and outputs
3. **Test dataset** (~10s examples) which tests if models can solve your task
4. **Unstructured dataset** with unlabelled data points related to the problem

You can modify the job description using any text editor and the datasets with any tables editor such as excel, google sheets, etc.

#### [HotpotQA Dataset](data/)
This directory contains task definitions for question answering using the [HotpotQA dataset](https://arxiv.org/abs/1809.09600). The tasks focus on developing models that can answer complex, multi-hop questions requiring reasoning across multiple documents. 


