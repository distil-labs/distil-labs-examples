# Refine the job description to train an SLM for classification

The **distil labs** platform allows anyone to use state-of-the-art methods for SLM fine-tuning. You do not need to be a machine learning expert to get a highly performant model customized to your needs in a day. 


## End-to-end workflow
This example demonstrates how to refine a job description for classification and then use it to train an SLM. You can iterate over the job description until our chosen 'teacher' LLM can solve the test dataset well enough. If a large language model (LLM) can solve a problem, we can then distil the ability of the LLM into a small model.

To complete the training, we will follow a [tutorial notebook](classification-how-to-write-job-description.ipynb) three-step process:

1. **Data Validation**: We start by uploading and validating our minimal dataset. To use distil labs, you need just a few examples per class and a problem description as discussed in [Data Preparation Guidelines for Classification](https://coconut-alto-537.notion.site/Data-Preparation-Guidelines-for-Classification-143fa0761dee80fca593e7a0bc4ee88e?pvs=4). 
2. **Teacher Evaluation**: In this step, we validate if an LLM can accurately solve the task. If the accuracy is too low, we will iterate on the task description to improve performance.
3. **SLM Training**: Finally, we will use all available labelled and unlabelled data to train a specialised SLM to match the performance of the LLM on our specific task.

