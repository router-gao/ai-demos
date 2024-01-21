# Environment

Ubuntu 22.04 

w/ or w/o GPU

16 vGPU, 32G RAM, 500G hardisk (thin provisioning)

The demo in this Confluence page is w/o GPU. 

# Conda installation

conda installation

```ubuntu
sudo apt-get update -y
sudo apt-get install -y build-essential
sudo apt-get install -y curl git wget
 
curl -sL "https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh" > "Miniconda3.sh"
bash Miniconda3.sh
```

create textgen context

```bash
source ~/.bashrc
conda create -n textgen python=3.10.9
conda activate textgen
```

# Jupyter notebook installation 

**The following steps are all in Conda textgen context.**

install PyTorch for CPU only env.

```shell
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
```

install PyTorch for GPU env.

```bash
pip3 install torch torchvision torchaudio
```

Install text-generation-webui. It's an optional process, while still highly recommended.

install text-generation-webui

```bash
git clone https://github.com/oobabooga/text-generation-webui
cd text-generation-webui
pip install -r requirements.txt
```

Start text-generation-webui, it's optional

```bash
conda activate textgen
cd text-generation-webui
python server.py  --share
```

Deploy Jupyter notebook

```bash
pip install notebook
jupyter notebook --generate-config
jupyter notebook password
```

Edit the fine '~/.jupyter/jupyter_notebook_config.py', and add the below parameters to it.

**jupyter_notebook_config.py**

```python
c.NotebookApp.ip = '0.0.0.0'
c.NotebookApp.port = 8888
c.NotebookApp.open_browser = False
c.NotebookApp.allow_root = True  # Only if you want to run as root
```

To start Jupyter Notebook

```bash
jupyter notebook
```

Login to the webpage and create Hello world [http://machine-ip:8888](http://machine-ip:8888/) or http://machine-ip:8888/lab

Get familiar with the functions.

![image-20240121105834566](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240121105834566.png)

# fine-tuning quick demo (w/o GPU)

Copy the code below to try Jupyter Notebook functions.

To register a wandb account, the document is here. (31 - wandb registration and sample charts)

w/o GPU, this fine-tuning demo may run 30 minutes or more.

finetuning-example.python

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

