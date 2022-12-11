# Modified Quoter Experiments

This is the GitHub repository for our term project in CS492: Introduction to Deep Learning. This is heavily inspired from our selected paper's original GitHub repository, which is located in this link: https://github.com/thunlp/QuoteR.

In this repository, we exhibit our main contributions and novel modifications, summarized below:
- A reduced dataset size by around 10%, to accommodate the team's inabundant resources.
- A modified early stopping algorithm for the first training function that calculates the accuracy of the model.
- Experiments on altered methods of generating context-quote pairs.

# Files Hierarchy
This GitHub repository is split into 2 major folders.
1. The **quoter** folder contains all the files for the training and testing pipeline. There are 6 .ipynb files for the training pipeline, all of which contain the exact same structure. The major difference is simply loading the corresponding dataset. These files are listed in detail below.
  - The English train/test pipeline for vanilla BERT
  - The English train/test pipeline for BERT-Sememe
  - The modern Chinese train/test pipeline for vanilla BERT
  - The modern Chinese train/test pipeline for BERT-Sememe
  - The ancient Chinese train/test pipeline for vanilla BERT
  - The ancient Chinese train/test pipeline for BERT-Sememe
2. Unfortunately, the model weights for all experiments are all too large to be uploaded to GitHub, so we attach the Google Drive link for the model weights here: https://drive.google.com/drive/folders/1oCw6mKI7id_T5aKXRlK1fuaKlARsETuM?usp=share_link
  - There are a total of 30 model weights for all experiments: there are 18 weights for the early stopping experiments and 12 weights for the context generation experiments. 
  - There are 6 weights for each pipeline in the early stopping experiments, and 4 weights for the context generation experiments.
4. Unfortunately, the dataset is too large to be uploaded to GitHub, so we attach the Google Drive link for the datasets here: https://drive.google.com/drive/folders/1d6dvWHMcqyaJ3enFLBZPjMefOD96PzaX?usp=share_link

# Interchanging Vanilla BERT and BERT-Sememe
You have to modify the transformers library directly in order to interchange between vanilla BERT and BERT-Sememe. In the transformers library, search for the __init__.py file and add the model BertSememeModel to the list of models to import in modeling_bert. Then, in the modeling_bert.py file, add all the contents of the modeling_bert_chinese.py file, if you are training for modern OR ancient Chinese. If you are training for English, add all the contents of the modeling_bert_english.py file. 

# Novel Parts of the Repository
The six pipeline files are modified accordingly as we progressed on our experiments. Below, you will see the major parts of the code that we reimplemented for the novel modifications we performed in this proposal.

## Reduced Dataset Size
This is accomplished mainly by reimplementing the _load_data_ function. We simply take 1000 context-quote pairs for our training, validation, and testing pipelines.

## Early Stopping Algorithm
This is accomplished by modifying the early stopping algorithm in the _training_ function. 

## Regeneration of Context-Quote Pairs
This is accomplished by changing the _make_context_tensors_ function, wherein we simply change the _sent_ local variable in the function to either **f + {MASK}** or **{MASK} + l**, depending on whether we are testing the only-former or only-latter context-quote pair generation.

# Important Points
1. The values saved in the models may not necessarily reflect the exact values reported in the paper. Since the original authors reported the best results of their experiments after multiple trials, we similarly chose the best results to display in our paper. However, you can freely run the pipelines and see the spontaneous results.
