---
language: en
license: mit
tags:
 - layoutlm
 - document-question-answering
 - pdf
---

# LayoutLM for Visual Question Answering

This is a fine-tuned version of the multi-modal [LayoutLM](https://aka.ms/layoutlm) model for the task of question answering on documents. It has been fine-tuned using both the [SQuAD2.0](https://huggingface.co/datasets/squad_v2) and [DocVQA](https://www.docvqa.org/) datasets.

## Getting started with the model

To run these examples, you must have [PIL](https://pillow.readthedocs.io/en/stable/installation.html), [pytesseract](https://pypi.org/project/pytesseract/), and [PyTorch](https://pytorch.org/get-started/locally/) installed in addition to [transformers](https://huggingface.co/docs/transformers/index).

```python
from transformers import AutoTokenizer, pipeline

tokenizer = AutoTokenizer.from_pretrained(
    "impira/layoutlm-document-qa",
    add_prefix_space=True,
)

nlp = pipeline(
    model="impira/layoutlm-document-qa",
    tokenizer=tokenizer,
    trust_remote_code=True,
)

nlp(
    "https://templates.invoicehome.com/invoice-template-us-neat-750px.png",
    "What is the invoice number?"
)
# {'score': 0.9943977, 'answer': 'us-001', 'start': 15, 'end': 15}

nlp(
    "https://miro.medium.com/max/787/1*iECQRIiOGTmEFLdWkVIH2g.jpeg",
    "What is the purchase amount?"
)
# {'score': 0.9912159, 'answer': '$1,000,000,000', 'start': 97, 'end': 97}

nlp(
    "https://www.accountingcoach.com/wp-content/uploads/2013/10/income-statement-example@2x.png",
    "What are the 2020 net sales?"
)
# {'score': 0.59147286, 'answer': '$ 3,750', 'start': 19, 'end': 20}
```

**NOTE**: This model was recently landed in transformers via [PR #18407](https://github.com/huggingface/transformers/pull/18407), so you'll need to use a recent version of transformers, for example:

```bash
pip install git+https://github.com/huggingface/transformers.git@5c4c869014f5839d04c1fd28133045df0c91fd84
```

The pipeline is currently in review ([PR #18414](https://github.com/huggingface/transformers/pull/18414)). In the meantime, you'll have to use the `trust_remote_code=True` flag to run it.

## About us

This model was created by the team at [Impira](https://www.impira.com/).
