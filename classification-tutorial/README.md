# Fine-tune a small language model for classification

The **distil labs** platform allows anyone to benefit from state-of-the-art methods for model fine-tuning. You don’t need to be a machine learning expert to get a highly performant model customized to your needs in a matter of a day. 


## End-to-end workflow
We will solve the routing task by going through the following process

1. **Task Definition**: We begin by defining our specific task by providing a small train/test dataset and the corresponding task description.
2. **SLM Training**: In this stage, we will validate if a large language model (LLM) can accurately solve our task, and if that is the case, we use all available data (both labelled and unlabelled) to train a specialized SLM to match the performance of the LLM.
3. **SLM Deployment**: Finally, we will receive our trained SLM binaries, and we can integrate them into our production environment. Note that deployment will be covered in the next notebook.
4. **SLM Retraining**: After deploying the first model, we can improve the performance of the initial model by providing additional training examples or by providing unlabeled contextual data. Note that we will not focus on retraining in this tutorial.


### Task Definition
You can use any of the four example problems to train your own model. Feel free to modify the example tasks to match your use-case os simply use them as they are! 

Each example dirctory outlined below contains the 4 main components of a task:
1. **Job description** that explains the classification task and describes all classes
2. **Train dataset** (~10s examples) which demonstrates our expected inputs and outputs
3. **Test dataset** (~10s examples) which tests if models can solve your task
4. **Unstructured dataset** with unlabelled data points related to the problem

You can modify the job description using any text editor and the datasets with any tables editor such as excel, google sheets, etc.


#### [Banking Customer Service Request Data](data-banking-routing/)
This directory contains task definitions for automated classification of banking customer service inquiries. The tasks focus on developing models to route customer support tickets to appropriate departments using the BANKING77 dataset structure.

#### [E-Commerce Product Data](data-ecommerce/)
This directory contains task definitions for classifying e-commerce product descriptions into four main categories: household items, books, clothing and accessories, and electronics. The tasks outline requirements for developing automated product categorization systems.

#### [Mental Health Comment Data](data-mental-health/)
This directory contains task definitions for mental health-related text classification problems. The tasks specify requirements for developing systems to categorize comments into mental health categories (Normal, Depression, Anxiety, Bipolar), with special considerations for handling sensitive content.

#### [Occupational Injury Data](data-injury/)
This directory contains task definitions for classifying workplace injury descriptions according to the Occupational Injuries and Illnesses Classification System (OIICS). The tasks outline requirements for mapping free-text injury narratives to seven standardized categories, including violence, transportation incidents, fires and explosions, and more.

### SLM Training
Use the [classification-training.ipynb](classification-training.ipynb) notebook to train a small language model (SLM) with the **distil labs** platform. We will follow a three-step process and, at the end, download our own SLM for local deployment.

To prepare for the training kick-off, modify the data in one of the examples directory (feel free to use excel/google sheets to edit the .csv files) or simply pick and example as is.

### Model Deployment

In the [classification-model-deployment.ipynb](classification-model-deployment.ipynb) notebook, we will deploy a trained classification small language model (SLM) with the **distil labs** platform. 

The model binaries can be downloaded using the `model` API by downloading the tarball and extracting into to the `model` directory.  The downloaded file will be called `*-model.tar`. Once extracted, you should find a `model/` directory which should be copied to the same directory as this notebook. At this point, your current working directory should look something like:

```
├── README.md
├── classification-model-deployment.ipynb
├── model
│   ├── config.json
│   ├── model.safetensors
│   ├── special_tokens_map.json
│   ├── tokenizer.json
│   ├── tokenizer_config.json
│   ├── training-logs.csv
│   └── training-logs.json
```

