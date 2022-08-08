---
language: en
thumbnail: https://uploads-ssl.webflow.com/5e3898dff507782a6580d710/614a23fcd8d4f7434c765ab9_logo.png
license: mit
---

# LayoutLM for Visual Question Answering

This is a fine-tuned version of the multi-modal [LayoutLM](https://aka.ms/layoutlm) model for the task of question answering on documents. It has been fine-tuned on

## Model details

The LayoutLM model was developed at Microsoft ([paper](https://arxiv.org/abs/1912.13318)) as a general purpose tool for understanding documents. This model is a fine-tuned checkpoint of [LayoutLM-Base-Cased](https://huggingface.co/microsoft/layoutlm-base-uncased), using both the [SQuAD2.0](https://huggingface.co/datasets/squad_v2) and [DocVQA](https://www.docvqa.org/) datasets.

## Getting started with the model

To run these examples, you must have [PIL](https://pillow.readthedocs.io/en/stable/installation.html), [pytesseract](https://pypi.org/project/pytesseract/), and [PyTorch](https://pytorch.org/get-started/locally/) installed in addition to [transformers](https://huggingface.co/docs/transformers/index).

```python
from transformers import AutoTokenizer, pipeline

tokenizer = AutoTokenizer.from_pretrained(
    "impira/layoutlm-document-qa",
    add_prefix_space=True,
    trust_remote_code=True,
)

nlp = pipeline(
        model="impira/layoutlm-document-qa",
        tokenizer=tokenizer,
        trust_remote_code=True,
)

nlp("https://templates.invoicehome.com/invoice-template-us-neat-750px.png", "What is the invoice number?")
# {'score': 0.9943977, 'answer': 'us-001', 'start': 15, 'end': 15}

nlp("https://miro.medium.com/max/787/1*iECQRIiOGTmEFLdWkVIH2g.jpeg", "What is the purchase amount?")
# {'score': 0.9912159, 'answer': '$1,000,000,000', 'start': 97, 'end': 97}

nlp("https://www.accountingcoach.com/wp-content/uploads/2013/10/income-statement-example@2x.png", "What are the 2020 net sales?")
# {'score': 0.59147286, 'answer': '$ 3,750', 'start': 19, 'end': 20}
```

**NOTE**: This model relies on a [model definition](https://github.com/huggingface/transformers/pull/18407) and [pipeline](https://github.com/huggingface/transformers/pull/18414) that are currently in review to be included in the transformers project. In the meantime, you'll have to use the `trust_remote_code=True` flag to run this model.

## About us

This model was created by the team at [Impira](https://www.impira.com/).
