---
title: "MLflow Prompt Registry and Evaluate for LLM-based OCR"
slug: mlflow-prompt-evaluate
tags: [evaluate, prompt-registry, ocr]
authors: [allison-bennett, shyam-sankararaman, michael-berk, mlflow-maintainers]
thumbnail: /img/prompt-evaluate.png
---

If you've tried your hand at Prompt Engineering, you understand it's more than meets the eye. Crafting an effective prompt is a nuanced skill, and lately it has become a priority to boost prompt and ML engineers productivity. Providing tools for these team members becomes vital for them to iterate and improve upon their prompts and agentic systems, while ultimately extracting the most value out of their GenAI applications. 

Today we will be showcasing how MLflow Prompt Registry and MLflow Evaluate can empower Prompt Engineers and ML Engineers alike to apply Optical Character Recognition (OCR) to scanned documents. Prompt iteration and evaluating the effectiveness and accuracy will be top of mind. 

## The Challenge with Prompting 
A good prompt engineer knows how to combine analytical thinking with creative approaches in order to gain the most out of their GenAI applications. This is all while ensuring the alignment with high level goals of their organization. To refine, iterate, and automate their process, they often need to have the technical skills that enable them to do so. How can we allow these prompt engineers to focus on the crafting of prompts, and less on the maintenance? 

There are also an abundance of challenges related to outputting and verifying the expected output. Did the prompt address the complexity of the situation? Did it have the appropriate context? Too much context? Did it introduce bias? 

Having a robust way to iterate on prompts and assess their accuracy becomes paramount to excelling in the world of prompting. 

## Introduction to OCR
Optical Character Recognition, or OCR, allows us to extract text from scanned documents and images. This texts ends up machine-encoded, editable, and searchable, opening up a variety of downstream use cases now that we can gain value from these sources. 

There are a few types of OCR ranging from Simple to Intelligent - today we will be focusing on the latter. This brings AI and ML into the mix to even further the capabilities for funcationality like handwriting recognition and adaptation to new styles. 

Fun fact - the earliest form of OCR was introduced in 1914, a device designed for blind indivuduals to read printed text without Braille called the Optophone. 
![Optophone](./margaret-hogan-used-the-black-sounding-optophone-to-read-a-book.webp)

## MLflow Concepts to Know
### MLflow Prompt Registry 
The release of MLflow 2.21.0 came the release of [MLflow Prompt Registry](https://mlflow.org/docs/latest/genai/prompt-version-mgmt/prompt-registry). Prompt Engineers now have a streamlined way to version, track, and reuse prompts. Let's look at a typical flow. 

**1. Create Your Prompt:** Each prompt is registered as a **Prompt Object**. This becomes your versioned, paramaterized template that can dynamically fill at runtime. Your object will include a **name** (unique identifier), your **template text**, a **version #**, the **commit message**, any **metadata/tags** (optional), and **aliases**. One reason MLflow Prompt Registry is so useful to Prompt Engineers is the version control capabilities. With a Git-inspired set up, prompt engineers are able to track, roll back, and compare their versions to maintain auditability and boost collaboration. 

Register your prompt with - 
```mlflow.genai.register_prompt()```

**2. Manage Aliases:** Aliases are a great way to ensure your prompts are meeting their intended use. For example...

**3. Load and Use Prompts:** We are not ready to load in our prompt and start use it it with tools like ... For this example, we will be using it directly with OpenAI's API, but other LLMs are available. 

Load in your prompt with - 
```mlflow.genai.load_prompt()```

### MLflow Evaluate 
MLflow evaluate is going to be key in our example today. This will allow us to systematically asses the performance of both traditional ML models and LLMs. Supporting both built-in and custom metrics, this becomes a useful tool in your model iteration. 

[Built-in metrics](https://mlflow.org/docs/latest/api_reference/python_api/mlflow.metrics.html) are a great way to get started. They are automatically computed based on your model type. The exact set will depend on your configurations, but you can generally expect Mean Absolute Error (MAE), Mean Absolute Percentage Error (MAPE), Maximum Residual Error (Max Error), Mean Squared Error (MSE), Root Mean Squared Error (RMSE), and R^2 scores for your regression models, and precision score, recall score, F1 score, accuracy score, and log loss for classificatio models. 

We also have built-in metrics for LLM and agent evaluation, allowing us to adhere by certain standards. You are able to follow traditional NLP metrics like BLEU and ROUGE, and LLM-judged metrics that will assess outputs like accuracy, relevance, and toxicity. 

Custom metrics can enable additional validations for traditional models, and really come in handy for our agentic workflows. You can do this by passing custom metric functions into the ```mlflow.evaluate``` API. The function signature is flexible, allowing us to pass in things like request, response, retrieved_context, expected_response, expected_facts, guidelines, expected_retrieved_context, trace, custom_expected, tool_calls, etc. This enables you to meet your company's evaluation criteria and scoring thresholds to ensure they are up to your standards. 

Results will all be logged in the MLflow run which can be accessed through the MLflow UI or programatically. 

We will see MLflow Evaluate in action as we walk through our OCR use case. 

### Additional Concepts 
While not central to this example, there are a few other MLflow functionalities that'll help along the way. 

**Tracking**
MLflow tracking allows you to log, organize, and visualize experiment results. This makes our result set more ingestable and auditable. 

**Tracing**
Tracing takes tracking one step further in order to have end-to-end observability for GenAI and agentic workflows. Again, this keeps everything organized as we work through and iterate on our workflows. 

**Autolog**
To make life simpler, ```mlflow.autolog()``` will reduce the need for manual log statements. Metrics, params, artifacts, and other useful information will be logged automatically. 

See [Further Reading](##Further-Reading) for some additional blogs digging into these concepts. 

## Our Use Case 
Our data consists of scanned documents and their corresponding text extracted as JSON. Our goal is to utilize LLMs to build a tool that will handle the text extraction for us.

## Setting it Up 

### Explore Our Data 

#### 1. Observe Data 

#### 2. Example LLM Call 

#### 3. Tracing UI 

### Create Model and Evaluate 

#### 1. Determine Accuracy 

#### 2. MLflow Evaluate 

#### 3. View in UI 

### Prompt Registry 

#### Prompt Engineer: Improve the Prompt 

#### ML Engineer: Use the Prompt 

## Configuration and Customization

## Conclusion and Next Steps

## Further Reading
