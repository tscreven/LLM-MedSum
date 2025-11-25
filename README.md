# LLM-MedSum
Fine-tuning and adaptation methods applied on T5-base with the purpose of summarizing academic medical articles on Pubmed.

To run this code in Google CoLab to use GPUs, Google Drive must be mounted. Add this cell as the first cell in every notebook:
```
# Change path to desired filepath.
path = "."
from google.colab import drive
drive.mount('/content/drive/' + path)
```

## Adaptation/Fine-tuning Method Notebooks
We applied fine-tuning and adaptation techniques to T5-base. Each fine-tuning
and adaptation technique has its own notebook, except for full fine-tuning and
SK-tuning which share one notebook. The name of each notebook represents the
adaptation method applied to T5-base. `baseline.ipynb` is T5-base without
any adaptations.

The only action users have to take to run the code is change the file location
the results are saved. The cell where users have to take action is the first
one:

```
# TODO: Change PATH to file location where you want results to be saved.
PATH = "."
```
* Note: Default is to strore results in the upper directory

After this, run all of the cells in the notebook in order to train (if
applicable) and then get the generated summaries. The notebook automaticaly
saves the generated summaries to the filepath the user inputs.

Training occurs in `SK-Tuning_Full-Finetuning.ipynb` (SK Tuning and Full Finetuning approaches are in this notebook) 
and `LoRA.ipynb`. Our recommendation would be to use a GPU to ensure a faster training process.

Brief descriptions of the model adaptation files file are as followed:

* `LoRA.ipynb` - Fine tuning approach which freezes the main model and inserts new layers, called low rank adaptors into the attention layers.

* `SK-Tuning_Full-Finetuning.ipynb` - Contains both the semantic knowledge fine tuning and fully finetuning approaches. Full fine tuning involves 
training all of the 220 million parameters that are there in T5-base. Semantic Knowlege tuning's training is less expensive as a small amount virtual prompt 
embeddings is trained. Here, that is 20 virtual tokens.

* `Retrieval.ipynb` - This file is for the hirarchial retrieval adaptation technique with the goal to try to find the sections that are the most relevant
(objective, methods, and conclusion. The Facebook AI Similarity Score metric (FAISS) was used for trying to reduce noise prior to the summarization process.

* `Oneshot.ipynb` - Python notebook for the one-shot prompting approach, which adds an input and output exemplar for in-context learning. This requires no
training.

## ModelResults.ipynb
Generates token and semantic similarity scores for model results. Creates tables and graphs displaying effectiveness of baseline and fine-tuning/adaptation techniques. 

Results are pulled from file path `DATA_LOCATION`. It defaults to the generated summaries used in the corresponding paper, but change path to evaluate other results in this cell:
```
DATA_LOCATION = 'Model_Summary_Texts/'
```
