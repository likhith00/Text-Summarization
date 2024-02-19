# Text-Summarization

This repository contains is implementation of text Summarization use case.

# README

## Finetuning google/t5-small for Text Summarization Downstream task

This repository contains code for finetuning the google/t5-small on a text summarization task with a dataset comprising english conversations with summaries.

### Task
- **Text Translation**: The task involves Summarizing the texts.

### Model
- **google/t5-small**: T5-Small is the checkpoint with 60 million parameters. The model is pre-trained on the Colossal Clean Crawled Corpus (C4). It is typically used for smaller-scale applications or environments where computational resources are limited, compared to larger variants like T5-base or T5-large. Despite its smaller size, it still maintains the ability to perform a wide range of text-related tasks effectively.

### Dataset
- **Dataset**: The dataset used is Truncated version of Samsum dataset.The SAMSum dataset has around 16,000 chat-like conversations along with summaries. Linguists, who are good at English, made these conversations. They were asked to make chats that are like the ones they have every day. The chats cover various topics, just like their real chats. The style and how formal they are can vary - some are casual, some are sort of formal, and some are formal. They might include slang, emojis, and mistakes. After that, the conversations were marked with summaries. These summaries are supposed to be short descriptions of what people talked about in the chat, but in third person.

### Libraries Used
- `transformers`: For utilizing and fine-tuning the Roberta-base model.
- `huggingface-hub`: For accessing the model and tokenizer from the Hugging Face model hub.
- `datasets`: For handling and processing the dataset.
- `numpy`: For numerical computations.
- `torch`: For building and training neural networks.
- `evaluate`:  For evaluating machine learning models or algorithms.
- `rouge_score`:  For computing ROUGE scores, commonly used in evaluating text summarization tasks.
- `py7zr`: For loading Samsum dataset. It is generally used for working with 7z archives, providing compression and decompression functionalities.

### Training Details
- **Pretrained Model**: google/t5-small
- **Weight Decay**: 0.01
- **Learning Rate**: 2e-5
- **Batch Size**: 16
- **Number of Epochs**: 10

### Results 

Here's the provided data formatted into a tabular format:

```
| Training Loss | Epoch | Step | Validation Loss | Rouge1 | Rouge2 | RougeL | RougeLSum | Gen Len |
|---------------|-------|------|-----------------|--------|--------|--------|------------|---------|
| No log        | 1.0   | 63   | 2.1165          | 0.338  | 0.1186 | 0.2811 | 0.2813     | 16.7595 |
| No log        | 2.0   | 126  | 2.0210          | 0.3612 | 0.1338 | 0.2982 | 0.2985     | 16.5592 |
| No log        | 3.0   | 189  | 1.9838          | 0.3652 | 0.1384 | 0.3034 | 0.304      | 16.1197 |
| No log        | 4.0   | 252  | 1.9623          | 0.3715 | 0.142  | 0.3077 | 0.3079     | 16.2308 |
| No log        | 5.0   | 315  | 1.9513          | 0.3727 | 0.1441 | 0.308  | 0.3084     | 16.1453 |
| No log        | 6.0   | 378  | 1.9419          | 0.375  | 0.1438 | 0.309  | 0.3093     | 16.2234 |
| No log        | 7.0   | 441  | 1.9376          | 0.3748 | 0.144  | 0.3102 | 0.3104     | 16.1465 |
| 2.2452        | 8.0   | 504  | 1.9324          | 0.3754 | 0.1451 | 0.3098 | 0.3099     | 16.1893 |
| 2.2452        | 9.0   | 567  | 1.9302          | 0.3769 | 0.1459 | 0.3112 | 0.3113     | 16.1966 |
| 2.2452        | 10.0  | 630  | 1.9294          | 0.3772 | 0.1453 | 0.3105 | 0.3106     | 16.1832 |
```

Each row represents a different step or epoch, and the corresponding values are placed under their respective columns.

### Usage
```
from transformers import pipeline

summarizer = pipeline("summarization", model="likhith231/T5-small-summarization")

text = "summarize: The Inflation Reduction Act lowers prescription drug costs, health care costs, and energy costs. It's the most aggressive action on tackling the climate crisis in American history, which will lift up American workers and create good-paying, union jobs across the country. It'll lower the deficit and ask the ultra-wealthy and corporations to pay their fair share. And no one making under $400,000 per year will pay a penny more in taxes."

print(summarizer(text))

```
