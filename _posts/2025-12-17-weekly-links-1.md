---
title: 'Weekly Links #1: [OPTIONAL THEME/TITLE]'
date: YYYY-MM-DD
permalink: /posts/2025/12/weekly-links-1/
tags:
  - weekly links
  - LLM
---

I scan all together too many papers, blog posts, and websites, so I figured I would make it mildly useful by making a selection of what I've read in the past week that may be interesting. From papers, to tech blogs, to LLMs, anything is game. Here is this week's post, and may it become a nice tradition. Happy reading!

---

## 1. Oopsie for fMRI

**Link:** https://www.nature.com/articles/s41593-025-02132-9#Ack1

**Type:** Paper

A study published in Nature Neuroscience that demonstrates that the basic tenet of fMRI studies, that increased brain blood flow is indicative of increased neuronal activity turns out to be untrue. Many regions have enough oxygen supply with baseline blood flow, and instead up their oxygen uptake from that blood upon higher neuronal activation. Many regions means **40%** of regions. This means that the thousands of studies that use fMRI with this assumption may need to be looked at again, particularly those drawing conclusions about the [Default Mode Network](https://neuroscientificallychallenged.com/posts/know-your-brain-default-mode-network) A key quote from the discussion section (BOLD = blood-oxygenation-level-dependent (signal), CBF = cerebral blood flow, OEF = oxygen extraction fraction, CRO2 = cerebral metabolic rate of oxygen, ∆ = change in):

> In this study, we evaluated the consistency between changes in the BOLD signal and oxygen metabolism in GM voxels across the human cortex. This would support the common interpretation of positive and negative ∆BOLD as indicators of increased or decreased neuronal activity. Contrary to the canonical BOLD response model, we found that approximately 40% of brain voxels with significant ∆BOLD exhibited opposing changes in oxygen metabolism. Specifically, voxels with positive ∆BOLD showed decreased ∆CMRO~2~, whereas those with negative ∆BOLD exhibited increased ∆CMRO~2~. By measuring the BOLD signal, CBF, OEF and CMRO~2~ in the same session, we uncovered distinct neurovascular mechanisms in regions with concordant versus discordant responses. Discordant voxels primarily regulate oxygen demand via ∆OEF, whereas concordant voxels display a larger increase in ∆CBF, aligning with canonical predictions. Moreover, discordant voxels demonstrated lower baseline CMRO~2~ and OEF, indicating that their baseline oxygen supply is sufficient to meet higher metabolic demands. In conclusion, we identified two distinct hemodynamic responses to neuronal activity changes, influenced by baseline OEF and metabolism.

See also the [University news article](https://www.tum.de/en/news-and-events/all-news/press-releases/details/40-percent-of-mri-signals-do-not-correspond-to-actual-brain-activity) and the [Bluesky threadpost](https://bsky.app/profile/vavatin.bsky.social/post/3ma4iffmp3s2d). 


---

## 2. Exfiltration of full LLM conversations of 8M+ users by shady browser extensions

**Link:** https://www.koi.ai/blog/urban-vpn-browser-extension-ai-conversations-data-collection

**Type:** Blog Post

An interesting case study that shows how hidden code in browser extensions that have 'featured' badges on the extension store brazenly extracts every interaction a user has with any of the big LLM providers by routing all requests though their own backend. They then sell this to analytics companies/[data brokers](https://www.wired.com/story/opinion-data-brokers-are-a-threat-to-democracy/). This is surely just one example among many. [Local, offline LLMs](https://hazyresearch.stanford.edu/blog/2025-11-11-ipw) can't mature fast enough.

---

## 3. Update on LLM performance for agentic coding 

**Link:** [[URL]](https://martinalderson.com/posts/are-we-in-a-gpt4-style-leap-that-evals-cant-see/)

**Type:** Blog Post

A nice blog post on how current LLMs are improving in ways that are not captured well by the benchmarks. For instance, Claude 4.5 Opus is much more capable of sticking to a plan and perform sensible defaults, and Gemini 3 Pro makes much nicer quality passable-good mock-ups for design work. Key quote:

> The second part - requiring less babysitting - I also expect most (all?) benchmarks don't test for. As far as I'm aware, benchmarks (by their nature) run a totally isolated environment with examples passing or failing. This doesn't actually really capture how at least I use coding agents. I don't just put it in yolo mode and have a very simple pass/fail for the task.
> 
> Instead it's a much more iterative process - making a plan, watching its output, interrupting it when I can see something that's not right.
>
> I really hope the industry starts adding more benchmarks like this. We're evaluating them like STEM students at a university exam. The world doesn't work like that - we need a bit more  qualitative 'taste' style benchmarking too for other roles.
> 
> This has been a subtle GPT-4 moment for me. I feel like I've got a whole new dimension of things I can build to an acceptable standard (design), and far more headspace to do it without constantly interrupting Claude.
>
> And this is where I think we start seeing the broader economic impacts of this. There's been a big disconnect between benchmark scores and hypothetical GDP growth when it comes to LLMs which has had a lot of people puzzled and has given a lot of ammunition to AI being a giant hype bubble. I (highly) suspect that the link is there, but we've just been doing the wrong benchmarks.

This agrees with [Simon Willison's thoughts on the matter (writing on the release of Claude Opus 4.5)](https://simonwillison.net/2025/Nov/24/claude-opus/). Perhaps we should all [just code our own little agent](https://fly.io/blog/everyone-write-an-agent/) with each model that comes out and have it try a few things. The models are [still not great at investing](https://stockbench.github.io/)...for now. 


---

## 4. The Universality of Neural Network Solutions: Similar Weights and Representations Across Models

**Link:** https://arxiv.org/abs/2512.05117

**Type:** Paper Series

Interesting set of papers on the universality of learned representations in neural networks, and learned weights on (fine-tuned) models for the same task (the platonic representation hypothesis, and universal weight subspace hypothesis, respectively):
* [This paper](https://arxiv.org/abs/2512.05117) sort of shows that you can compress many (fine-tuned) models to the same ~16-dimensional weight subspace and recover most of the function
* On how representations in SSL converge to similar ones except some linear transformation: [first paper here](https://arxiv.org/abs/2007.00810); [platonic hypothesis from last year](https://arxiv.org/abs/2405.07987); [here a paper](https://arxiv.org/html/2505.12540v2) that uses the fact that representations will be similar between different models trained on the same thing (here: text) to do completely unpaired translation given only embeddings and no paired data.
* [Hackernews topic on this](https://www.hacker-news.news/post/46199623)

---

## 5. In-depth tips for wrangling the Python pandas library like a pro

**Link:** https://github.com/chiphuyen/just-pandas-things/blob/master/just-pandas-things.ipynb

**Type:** Tutorial

Really nice zoom-in on the particulars of pandas. Some massive speed-ups are easily obtained if you know what's going on. I always naively used iterrows when I needed to, while itertuples does almost the same thing while being _much_ faster. Check out [Chip's blog](https://huyenchip.com/blog/) for more gems on genAI and LLMs. 

---
