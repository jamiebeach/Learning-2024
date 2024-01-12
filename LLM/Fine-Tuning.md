# Fine Tuning

## Resources (Videos, Links, Tutorials)
- [Fine-tuning Large Language Models (LLMs) | w/ Example Code](https://www.youtube.com/watch?v=eC6Hd1hFvos)
  - This is a great video from [Shaw Talebi](https://www.youtube.com/@ShawhinTalebi) that discusses what fine-tuning is and how to create and use a LoRAto fine-tune a language model. Shaw includes code examples in the video and very clearly described every line of code and parameter used.

## What is Fine-Tuning?

Fine-tuning a Large Language Model (LLM), such as [Mistral 7B](https://mistral.ai/news/announcing-mistral-7b/), involves adjusting and refining the model's parameters specifically for a particular task or to better suit specific data. This process is essential when you want the model to perform well on a specific type of data or task that might not be well-represented in the training data used for the initial, broad training of the model. Here's a more detailed look at the process:

1. **Pre-Trained Model**: LLMs are initially trained on a vast and diverse dataset. This training is general and aims to provide the model with a broad understanding of language and the ability to generate coherent and contextually appropriate text.

2. **Selecting a Task or Domain**: Fine-tuning is often task-specific. For instance, you might want to fine-tune a model for medical text analysis, customer service chatbots, legal document review, or another specialized task. The choice of task will guide the fine-tuning process.

3. **Gathering Task-Specific Data**: Once a task is selected, you need a dataset that is representative of this task. For example, if you're fine-tuning a model for medical purposes, you would gather a large dataset of medical texts.

4. **Training (Fine-Tuning) Process**: The pre-trained model is then further trained (fine-tuned) on this new, task-specific dataset. During this process, the model's parameters (weights) are slightly adjusted so that the model becomes better at generating or understanding text in the context of the chosen task. This process doesn't usually require as much computational power or time as the initial training, since the model is already knowledgeable in general language understanding.

5. **Evaluation and Iteration**: After fine-tuning, the model's performance is evaluated on a separate set of task-specific data that wasn't used during training. This helps to ensure that the model can generalize well to new, unseen data in the same domain. If the performance isn't satisfactory, further iterations of fine-tuning might be necessary, possibly with adjustments in the training data or fine-tuning procedure.

6. **Application**: Once fine-tuned, the model is ready to be deployed in applications specific to the task it was trained for, with improved performance and accuracy in that domain compared to the original, non-fine-tuned model.

Fine-tuning allows for the customization of large, general-purpose language models to specific needs and domains, making them more useful and effective in specialized applications.

## Advantages

- A smaller fine-tuned model can often out-perform a larger base model

## LoRA

- Low-Rank Adaptation model
- Augments the base model with new trainable parameters
