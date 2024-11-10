---
title: 'Foundation model sources starter kit'
date: 24-11-10
permalink: /posts/2024/11/foundation-model-links/
tags:
  - Foundation models
  - BioML
  - self-supervised representation learning
  - scGPT
  - causal machine learning
  - good (bio)ML blogs
---

**Dieter Stoker**  
*Originally created 05-06-2024 to onboard some new de Ridder lab members in the foundation model domain*

Hi, thanks for clicking! I thought I’d make a nice collection of resources that I find pertinent ~halfway through 2024 in the field of BioML, with a slant towards foundation models and good educational materials. This is a reproduction of my Notion page [here](https://nebulous-booth-32c.notion.site/Foundation-models-tips-and-links-432e39f183e242ba9a144df1357189a1)

---

### TL;DR
#### What is most salient among all of this? I think:
- [The Road to Biology 2.0](https://freedium.cfd/https%3A%2F%2Ftowardsdatascience.com%2Fthe-road-to-biology-2-0-will-pass-through-black-box-data-bbd00fabf959)
- [Position of ML in Science](https://arxiv.org/abs/2405.18095) (general oversight)
- [DL gone wrong examples](https://www.nature.com/articles/s42256-020-00257-z)
- [The Bitter Lesson](https://www.cs.utexas.edu/~eunsol/courses/data/bitter_lesson.pdf) (more data/compute often trumps human solutions); Counterpoint: [A Better Lesson](https://rodneybrooks.com/a-better-lesson/)
- [Scaling hypothesis](https://gwern.net/scaling-hypothesis) for big model hype; Counterpoint: [Against big model hype](https://arxiv.org/abs/2304.15004) and [Techno-optimism](https://arxiv.org/abs/2405.07987)
- [Step-by-step with NNs](http://karpathy.github.io/2019/04/25/recipe/)
- Variational Autoencoders (VAEs): [Explanation 1](https://towardsdatascience.com/understanding-variational-autoencoders-vaes-f70510919f73), [Explanation 2](https://www.jeremyjordan.me/variational-autoencoders/), [Paper](https://arxiv.org/pdf/1606.05908)
- [Self-supervised learning paper](https://ieeexplore.ieee.org/abstract/document/9770283)
- [Causal ML exists](https://www.nature.com/articles/s41467-020-17419-7)
- [Biological foundation models overview](https://arxiv.org/abs/2311.07621)
- [Manifold learning](https://www.sciencedirect.com/science/article/pii/S2452310017301877) ([TopOMetry](https://www.biorxiv.org/content/10.1101/2022.03.14.484134v3.abstract) if you dare)
- [NN Manifolds Topology basics](https://colah.github.io/posts/2014-03-NN-Manifolds-Topology/)
- [Primers on single-cell foundation models](https://www.abhishaike.com/p/the-lore-behind-scrna-seq-foundation-models) and [Scaling Laws of Agency](https://markovbio.github.io/scaling-laws-of-agency/)
- [Limits in BioML](https://www.biorxiv.org/content/10.1101/2023.10.16.561085v2) and [Another perspective](https://www.biorxiv.org/content/10.1101/2024.04.02.587824.abstract)
- Researchers: [Marinka Zitnik](https://zitniklab.hms.harvard.edu/), [Mihaela van der Schaar](https://www.vanderschaar-lab.com/publications/), [Fabian J Theis](https://www.helmholtz-munich.de/en/icb/research-groups/theis-lab), [Bo Wang](https://www.wanglab.ai/research.html), [Mohammad Lotfollahi](http://lotfollahi.com/research), and [Pietro Liò](https://scholar.google.nl/citations?user=4YhNJBEAAAAJ&hl=en&oi=ao) on hypergraphs.

---

### A step back: when is ML useful? What can go wrong?
- [Utility and pitfalls of ML in science](https://arxiv.org/abs/2405.18095)
- [Lack of empirical rigour in ML](https://openreview.net/forum?id=rJWF0Fywf&source=post_page---------------------------)
- [Shortcut learning in DL](https://www.nature.com/articles/s42256-020-00257-z)
- [Pitfalls of ML](https://www.nature.com/articles/s41576-021-00434-9#Sec15)
- [ML in medical practice (European)](https://ieeexplore.ieee.org/abstract/document/9783196)
- [Explainability debate](https://www.nature.com/articles/s42256-019-0048-x) and follow-up [discussion](https://projecteuclid.org/journals/statistics-surveys/volume-16/issue-none/Interpretable-machine-learning-Fundamental-principles-and-10-grand-challenges/10.1214/21-SS133.full)
- [Emergent abilities in language models](https://arxiv.org/abs/2304.15004) with follow-up [showing in-context learning](https://arxiv.org/abs/2309.01809)

---

### The *n* horsemen of the Single Cell Foundation Model-pocalypse
- scGPT: [scGPT](https://www.nature.com/articles/s41592-024-02201-0)
- [GeneFormer](https://www.nature.com/articles/s41586-023-06139-9.epdf?sharing_token=u_5LUGVkd3A8zR-f73lU59RgN0jAjWel9jnR3ZoTv0N2UB4yyXENUK50s6uqjXH69sDxh4Z3J4plYCKlVME-W2WSuRiS96vx6t5ex2-krVDS46JkoVvAvJyWtYXIyj74pDWn_DutZq1oAlDaxfvBpUfSKDdBPJ8SKlTId8uT47M=)
- [Universal Embeddings](https://www.biorxiv.org/content/10.1101/2023.11.28.568918v1.abstract)
- [scFoundation](https://www.biorxiv.org/content/10.1101/2023.05.29.542705v4)
- [NicheFormer](https://www.biorxiv.org/content/10.1101/2024.04.15.589472v1)
- [CellFM](https://www.biorxiv.org/content/10.1101/2024.06.04.597369v1)
- [Awesome Foundation Model Single Cell Papers](https://github.com/OmicsML/awesome-foundation-model-single-cell-papers)

---

### Courses/textbooks/learning materials
- [D2L](https://d2l.ai/)
- [MIT's Deep Learning Course](http://introtodeeplearning.com/)
- [Neural Networks and Deep Learning](http://neuralnetworksanddeeplearning.com/)
- [Understanding Deep Learning](https://udlbook.github.io/udlbook/)
- [Stanford NLP Course](https://web.stanford.edu/class/cs224n/index.html#coursework)
- [Alice in Differentiable Wonderland](https://www.sscardapane.it/alice-book)

---

### Libraries
- [scvi-tools](https://github.com/scverse/scvi-tools)
- [Pyro](http://pyro.ai/)
- [Pytorch Lightning](https://lightning.ai/docs/pytorch/stable/)
- [Weights and Biases](https://wandb.ai/site)

---

### LLMs
- [Jargon-free LLM explanation](https://arstechnica.com/science/2023/07/a-jargon-free-explanation-of-how-ai-large-language-models-work/)
- [Big Survey on LLMs](https://arxiv.org/abs/2307.06435)
- [LLMs from scratch](https://github.com/rasbt/LLMs-from-scratch)
- [Transformers Illustrated](https://jalammar.github.io/illustrated-transformer/)
- [FineWeb](https://huggingface.co/spaces/HuggingFaceFW/blogpost-fineweb-v1)
- [Open source LLM history](https://cameronrwolfe.substack.com/p/the-history-of-open-source-llms-early)

---

### Mechanistic Interpretability
- [Neel Nanda's Work](https://www.neelnanda.io/mechanistic-interpretability/quickstart)
- [Transformer Circuits](https://transformer-circuits.pub/)
- [Interpretability Overview](https://arxiv.org/abs/2405.00208)

---

### Youtube Channels/Playlists
- [AI Coffee Break](https://www.youtube.com/@AICoffeeBreak)
- [Yannic Kilcher](https://www.youtube.com/@YannicKilcher)
- [Andrej Karpathy](https://www.youtube.com/@AndrejKarpathy)
- [Efficient NLP](https://www.youtube.com/playlist?list=PLgJhDSE2ZLxa3qLAJ8VU_9u-cx0I9tQMd)
- [Weights and Biases Talks](https://www.youtube.com/@WeightsBiases)

---

**END OF KIT**. I hope you find something here that’s useful!
