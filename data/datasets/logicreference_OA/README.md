# LogicInference Dataset

This repository contains the Python code used to generate the `LogicInference`
dataset. `LogicInference` is a dataset designed to evaluate the ability of
models to perform logical inference. The dataset focuses on inference using
propositional logic and a small subset of first-order logic, represented both in
semi-formal logical notation, and in natural language. `LogicInference` has two
main long-term goals: (1) to evaluate the ability of models to perform logical
inference, and the degree to which inference chains are real or hallucinated,
and (2) to assess whether learning logical inference abilities in the abstract
(e.g., getting better in this dataset) would then transfer to other real-world
tasks.

For a detailed description of the dataset, please check the following paper:
https://openreview.net/pdf?id=HAGeIS_Lcg9 (arXiv preprint:
https://arxiv.org/abs/2203.15099 )

Please cite as:

```
@inproceedings{ontanon2022logicinference,
  url = {https://openreview.net/pdf?id=HAGeIS_Lcg9},
  author = {Onta\~{n}\'{o}n, Santiago and Ainslie, Joshua and Cvicek, Vaclav and Fisher, Zachary},
  title = {{LogicInference}: A New Dataset for Teaching Logical Inference to seq2seq Models},
  booktitle={Proceedings of ICLR 2022 workshop on Objects, Structure and Causality},
  year={2022}
}
```

This is an re-produce of the dataset from LogicInference Dataset in paper:
https://openreview.net/pdf?id=HAGeIS_Lcg9.

The github page of LogicInference Dataset:
https://github.com/google-research/google-research/tree/master/logic_inference_dataset.

This dataset is aimed to offer more dataset for Open Assistant project,
depending on their demands, there three columns: INSTRUCTION, RESPONSE, SOURCE.

The results in this dataset is a little different from which was introduced in
the original paper:

1.For all three splits (IID/OOD/length), only IID is used. In the original
paper, it seems that model can reach better performance with data generated by
this split method.

2.In the original paper, there are two form of responses:
LOGICINFERENCE<sub>b</sub> (with the answer at the beginning) and
LOGICINFERENCE<sub>e</sub> (with the answer at the end). This dataset uses
LOGICINFERENCE<sub>e</sub>, that means: for all questions, the model will first
do logic inference, and give the final answer at the end.

3.The original paper, some parameters in generate_dataset.py are:

N_INFERENCE_PROBLEMS = 5000

N_VARIATIONS = 25

N_EXAMPLES = 200000

TRAIN_RATIO = 0.9

LENGTH_SPLIT_THRESHOLD = 4

RANDOM_SEED = 0

I choose some new parameters:

N_INFERENCE_PROBLEMS = 10000

N_VARIATIONS = 25

N_EXAMPLES = 55000

TRAIN_RATIO = 1

LENGTH_SPLIT_THRESHOLD = 4

RANDOM_SEED = 1111

The original script generated 4814 different inference problems and extended all
those inference problems to around 200,000 Q-A pairs. My settings generated 5491
different inference problems and extended them to around 54,607
Instruction-Response pairs. I think for Open Assistant projects, maybe the
number of different inference problems is more important, and generated many
similar Instruction-Response pairs will only add training time and doesn't make
much sense.

4.I only keep the generate_dataset.py file in this directory, because the coding format of the original project does
not fit OA project which need flake8 format. I only change the coding format of generate_dateset.py.