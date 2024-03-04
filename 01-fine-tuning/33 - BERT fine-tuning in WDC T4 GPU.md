
**The demo is made as a fine-tuning foundation.**

**To make the demo running fast and consume less resource, the find-tuning args and process are simplified purposely.**

## Environment

- Ubuntu 22.04 LTS desktop

- 16 vGPU and 32G RAM, 500G thin hard disk.

- T4 GPU is passthrough. NVIDIA-SMI 535.86.05              Driver Version: 535.86.05    CUDA Version: 12.2  

- Model is ''bert-base-cased' and 'bert-base-uncased', huggingface format (HF).


Dataset is huggingface glue/cola

https://huggingface.co/datasets/glue/viewer/cola/test_matched

Step by step configuration videos is here.

https://drive.google.com/file/d/1NahHW20bNoKyWgzFQA7tZ3icfjP3q7o8/view?usp=sharing

## Introduction of BERT

https://github.com/google-research/bert

There are 2 fine-tuning process in this articles. And use the same validation script to test both tuned model to demo the difference between 'cased' model and 'uncased' model.

The fine-tuning process is simplified, and both model 'bert-base-cased' and 'bert-base-uncased' are using the same training_args and same Dataset.

Fine-tuning script for bert-base-cased.

```python
from transformers import BertForSequenceClassification, BertTokenizerFast, Trainer, TrainingArguments
from datasets import load_dataset
 
# 1. Load tokenizer and model
tokenizer = BertTokenizerFast.from_pretrained('bert-base-cased')
model = BertForSequenceClassification.from_pretrained('bert-base-cased')
 
# 2. Load dataset and tokenize
dataset = load_dataset("glue", "cola")
tokenized_ds = dataset.map(lambda x: tokenizer(x['sentence'], truncation=True, padding='max_length', max_length=128), batched=True)
 
# 3. Set up training arguments
training_args = TrainingArguments(
    output_dir = "./fine_tuned_bert_cased",
    evaluation_strategy = "epoch",
    per_device_train_batch_size=16,
    per_device_eval_batch_size=64,
    num_train_epochs=3,
    learning_rate=3e-5,
    warmup_steps=500,
    weight_decay=0.01,
    logging_dir='./logs'
)
 
# 4. Fine-tune model
trainer = Trainer(
    model=model,
    args=training_args,
    train_dataset=tokenized_ds['train'],
    eval_dataset=tokenized_ds['validation']
)
 
trainer.train()
 
# 5. Evaluate model
result = trainer.evaluate()
print(result)
 
# 6. Save model
trainer.save_model("./fine_tuned_bert_cased")
```

![image-2023-9-20_23-24-17](https://github.com/router-gao/ai-demos/assets/144886373/8773c0d1-ae4b-4291-83c2-b4d197f38193)

![image-2023-9-20_23-25-27](https://github.com/router-gao/ai-demos/assets/144886373/072aca62-0ebb-4e74-ab75-a1d11c6ac23f)

 

The validation script is as below. There are 5 senteces, and some words are start with capital letter to confuse the model.

**validation**

```python
from transformers import BertForSequenceClassification, BertTokenizerFast
 
# Load tokenizers and models
tokenizer_cased = BertTokenizerFast.from_pretrained('bert-base-cased')
model_cased = BertForSequenceClassification.from_pretrained("./fine_tuned_bert_cased")
 
tokenizer_uncased = BertTokenizerFast.from_pretrained('bert-base-uncased')
model_uncased = BertForSequenceClassification.from_pretrained("./fine_tuned_bert_uncased")
 
# Updated test sentences
test_sentences = [
    "The Row in the theater was near the lake where they row their boat.",
    "I will Object to the placement of that strange object in the room.",
    "He loves Apple products.",
    "Let Read read the book with a red cover next week.",
    "I will Present my ideas during the present meeting."
]
 
# Define prediction functions for both models
def get_prediction_cased(text):
    inputs = tokenizer_cased(text, truncation=True, padding=True, max_length=128, return_tensors="pt")
    outputs = model_cased(**inputs)
    return 'Correct' if outputs.logits.argmax(dim=1).item() == 1 else 'Incorrect'
 
def get_prediction_uncased(text):
    inputs = tokenizer_uncased(text, truncation=True, padding=True, max_length=128, return_tensors="pt")
    outputs = model_uncased(**inputs)
    return 'Correct' if outputs.logits.argmax(dim=1).item() == 1 else 'Incorrect'
 
# Evaluate the test sentences using both models
predictions_cased = [get_prediction_cased(sentence) for sentence in test_sentences]
predictions_uncased = [get_prediction_uncased(sentence) for sentence in test_sentences]
 
print("Sentences:", test_sentences)
print("Cased Model Predictions:", predictions_cased)
print("Uncased Model Predictions:", predictions_uncased)
```



From the output of both tuned models, 'cased' model can read the letters with Capital letter.

**validation output**

```shell
(textgen) ubuntu@ubuntu-vm:~/Downloads$ python test-cases.py
Sentences: ['The Row in the theater was near the lake where they row their boat.', 'I will Object to the placement of that strange object in the room.', 'He loves Apple products.', 'Let Read read the book with a red cover next week.', 'I will Present my ideas during the present meeting.']
Cased Model Predictions: ['Incorrect', 'Incorrect', 'Correct', 'Incorrect', 'Incorrect']
Uncased Model Predictions: ['Correct', 'Correct', 'Correct', 'Incorrect', 'Correct']
(textgen) ubuntu@ubuntu-vm:~/Downloads$
```



# Conclusion

Select the right model for the right task.

