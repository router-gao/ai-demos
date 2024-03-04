**The demo is made as a fine-tuning foundation.**

**To make the demo running fast and consume less resource, the find-tuning args and process are simplified purposely.**

## Environment

- Ubuntu 22.04 LTS desktop
- 16 vGPU and 32G RAM, 500G thin hard disk.
- T4 GPU is passthrough. NVIDIA-SMI 535.86.05              Driver Version: 535.86.05    CUDA Version: 12.2  

- Model is GPT2 (another name is gpt2-tiny), huggingface format (HF).

- Dataset is huggingface ag_news.

- wandb statistics graphs




## The fine-tuning python script

GPT2 fine-tuning script

```python
from datasets import load_dataset
from transformers import GPT2Tokenizer, GPT2LMHeadModel, Trainer, TrainingArguments
 
# Load AG News dataset from Hugging Face's datasets library
dataset = load_dataset("ag_news")
 
# Tokenizer initialization
tokenizer = GPT2Tokenizer.from_pretrained("gpt2")
tokenizer.pad_token = tokenizer.eos_token
 
# Convert the datasets to the format suitable for GPT-2
def tokenize_function(examples):
    output = tokenizer(examples['text'], padding='max_length', truncation=True, max_length=128)
    return {
        'input_ids': output['input_ids'],
        'attention_mask': output['attention_mask'],
        'labels': output['input_ids']  # Set labels to input_ids for language modeling
    }
 
tokenized_train_dataset = dataset["train"].map(tokenize_function, batched=True)
tokenized_test_dataset = dataset["test"].map(tokenize_function, batched=True)
 
# Model Preparation
model = GPT2LMHeadModel.from_pretrained("gpt2")
 
# Fine-tuning
training_args = TrainingArguments(
    per_device_train_batch_size=32,
    per_device_eval_batch_size=32,
    num_train_epochs=1,
    logging_dir="./logs",
    logging_steps=10,
    save_steps=10,
    evaluation_strategy="steps",
    eval_steps=500,
    save_total_limit=2,
    output_dir="./results"
)
 
trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=tokenized_train_dataset,
    eval_dataset=tokenized_test_dataset
)
 
trainer.train()
 
# Evaluation
results = trainer.evaluate()
 
print(results)
   
```

 

## Validating

validating python script

```python
from datasets import load_dataset
from transformers import GPT2Tokenizer, GPT2LMHeadModel, pipeline
 
# 1. Load the fine-tuned model and tokenizer
model_path = "/home/ubuntu/Downloads/results/checkpoint-3750"
model = GPT2LMHeadModel.from_pretrained(model_path)
tokenizer = GPT2Tokenizer.from_pretrained("gpt2")
tokenizer.pad_token = tokenizer.eos_token
 
# 2. Create a text generation pipeline
text_generator = pipeline("text-generation", model=model, tokenizer=tokenizer, device=0)  # use device=0 for GPU
 
# 3. Load AG News test dataset
dataset = load_dataset("ag_news", split="test")
texts = dataset["text"]
 
# 4. Generate predictions
for text in texts[:10]:  # Testing on first 10 samples, adjust as needed
    input_text = text[:100]  # Use the first 100 characters as a prompt
    generated_text = text_generator(input_text, max_length=150, do_sample=True, top_k=50)
    print(f"Input: {input_text}")
    print(f"Generated: {generated_text[0]['generated_text']}\n")
```

 

## Lessons Learned

ChatGPT4 is more sharper than Claude2 in assisting fine-tuning
Prompting 'simplify the script' is better than 'fix the issue' or 'solve the problem'
training_args plays the magic
select the right pre-tuned model is critical
