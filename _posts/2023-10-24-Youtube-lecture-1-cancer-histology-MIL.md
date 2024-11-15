---
title: 'Youtube lecture notes #1: (hilarious) multiple-instance learning on cancer histopathology slides flash talk'
date: 2023-10-24
permalink: /posts/2023/10/cancer-histology-MIL/
tags:
  - Youtube lecture notes
  - multiple-instance learning
  - cancer histopathology
  - self-supervised representation learning
  - flow cytometry
  - weakly supervised learning
---

Link: [https://www.youtube.com/watch?v=zOD2Wt0pTRQ](https://www.youtube.com/watch?v=zOD2Wt0pTRQ)


## TL;DR

* Multiple-instance learning is a problem where there is some top-level labeled object (a patient who is a responder or non-responder to some drug, say, or a huge pathology image slide which as a whole either has cancer tissue or not) which is made up of component parts that we measure, but none of which individually per se lead to the top-level label (for flow cytometric measurements of immune cells in Acute Lymphoblastic Leukemia: a patient as a bag of cells, some of which are malignant; for tissue slides: slide image tiles that together make up the whole image, where some might have tumor material whereas others have none).

* In cancer histopathology slide classification, the data is simply too large to be processed all at once. Hence, we must resort to cutting the image up into tiles, and working on those.

* However, tile-based methods suffer from important drawbacks: they are weakly labeled (slide-level labels like cancer/not-cancer don’t translate to tile-level labels), and miss spatial context.

* Self-supervised representation learning, such as contrastive learning methods, can use encoder-decoder architectures combined with losses to bring encoded versions of the same tile with slightly different modifications (croppings/rotations/transformations/addition of random noise) close, while staying further from that of a different tile, to learn informative tile-level representations in much fewer dimensions (think 1,024*1,024*3 to 1,000) This requires no tile-level labels whatsoever.

* With this learned dimensionality reduction in hand, we can encode all tiles of a top-level image, stitch them back together, and use a second neural network to now do the classification based on these features. This means spatial context can be taken into account (the second model can learn these realtions) and that we now are back to the one sample : one label-scenario that we know and love.

## Introduction  
Welcome to the first installment of Youtube lecture notes, where I make a write-up of an interesting Youtube lecture.  
I was interested in this talk because of the often-recurring talk of multiple-instance learning (MIL, not to be confused with Mother-In-Law) as a possible solution to our problems in the biomedical field. While the talk focuses on images, similar problems occur everywhere. In a nutshell, the issue is that you have a huge thing (with a label) made up of many smaller instances (generally without a label), and the exact make up of these smaller instances (amount, features) might be quite different between different huge things. Let’s call our huge things ‘patients’ and our smaller instances ‘cells’. If we do, say, flow cytometry analysis, we measure marker expression on many cells, and each patient is then represented as a collection or bag of such cells. Such is the human condition: we are all but bags of cells. Now, we have patient-level labels, namely healthy or diseased, or good prognosis versus bad prognosis, or responder and non-responder, and we have multiple instances per patient. How do we learn a classifier that can recognize whether a patient is type A or B, given that we assume there is some structure in the instances that differentiates patients A from B, but we don’t know it: the classifier should figure it out. That is what MIL tries to do. In image slides, this comes back as **HUGE** high-resolution pathology slide images that might contain tumour cells somewhere, but we don’t know where. We just know it is from cancerous tissue. We might also have such slices from healthy tissue. For automated analysis, you can think of an image as a collection of patches, and the task becomes to classify images as cancerous or non-cancerous based on such collections of patches. Again: a label on the level of the huge object (complete image), real information that causes/is correlated with that label in the various instances (image patches), up to the classifier to learn to identify images that are and are not cancerous based on them automagically.  
I have to say that James Leech is a dramaturge without equal and made this talk very fun. Kudo’s to him! Let’s get to the meat and bones of the matter.


## Image analysis for cancer diagnosis

Cancer pictures can easily be 3 Gb. Hence, treating images as bags of patches is necessary even from a practical point of view. You simply can’t put images of such magnitude in the memory for training batches for a neural network!  
Going further, MIL is a part of weakly supervised learning. If you have an image slide, then the slide-level label is cancer. But only a few patches of the image have information on that, and many have irrelevant information. For instance, in the image below ([source](https://images.squarespace-cdn.com/content/v1/5c308af3f2e6b1bd0e605a39/1594427325365-AFB1PUPX50WLMT4EXRY1/Basal+Cell+Carcinoma%2C+Andreas+Astier.)), images that contain white space or barely any tissue at all will also have the label cancer but the model should disregard such images.



| ![](/images/blog_post_1/Slide_to_tile.png)| 
|:--:| 
| Figure 1. A basal-cell carcinoma histpathology slide, divided into tiles. The slide-level label is clear, but the separate tile probably does not have any information salient for cancer/not-cancer classification. If you were to naively give every tile the top-level label and train a classifier, you'd have a bad time. Image taken from [here](https://images.squarespace-cdn.com/content/v1/5c308af3f2e6b1bd0e605a39/1594427325365-AFB1PUPX50WLMT4EXRY1/Basal+Cell+Carcinoma%2C+Andreas+Astier). |


Another problem is that you might want to take into account the spatial proximity in the patches for your classification. However, since you divide the image into patches, you can’t work like that.

## Inference

Let’s say you train on this per-tile level anyway. You get a per-tile classification. How do you now aggregate the per-tile classifications to get a total classification? Well, there is no set way to go about that. If you expect that there are quite some positive tiles (in the slide above there is an abundance of tumour cells), and you think they are uniformly distributed, you might do some averaging or voting. If the tiles with useful information are very rare, then you might want to go with an activation function-like approach, where negatives weigh very little in the decision, but one positive tile counts for a lot. If you are very concerned about false negatives, you might instead go for saying that even 1 positive tile classifies the sample as cancerous. However, picking the approach requires some sort of domain knowledge and requires manual work.

| ![](/images/blog_post_1/Combining_tiles.png)| 
|:--:| 
| Figure 2. Combining the tiles requires some sort of domain knowledge on what matters for your specific problem area. Do you do some sort of voting? Heavily weight any positive occurrence over negative patches? Say that even one positive patch means a whole-slide positive label since you don't want false negatives? This requires manual fiddling. |

## Problems so far

So there’s two main problems here:

1. We can’t deal with whole images at once. However, training a tile-level classifier is difficult: many tiles are not informative for the top-level label, and you miss context (since you remove spatial information by acting like a slide is a bag of images).

2. if you manage to train a tile-level classifier, how to aggregate the results depends on your exact question and domain expertise, making this a difficult and fraught process.

## Contrastive learning to the rescue  
Contrastive learning can ease these issues. Contrastive learning is one of the main classes of methods in self-supervised (representation) learning (SSRL), the other one being masking (such as used in Large Language Models. see [here](https://ieeexplore.ieee.org/abstract/document/9770283) for a great overview of SSRL. The approach simply boils down to the intuition that different (noisy/cropped/transformed) versions of the same image (patch) should lead to more similar neural-network based feature encodings than that of another patch, no matter what the label. Below, an example is given of two different croppings of one image (a cute cat), which should be different from that of another image ( a cute dog). We can implement this without labels: it would hold even if the image on the right were of another cat: different image croppings of the same cat should be more similar to each other than to those of another cat. We could do the same thing with pathology slide image tiles!


| ![](/images/blog_post_1/Contrastive_learning.png)| 
|:--:| 
| Figure 3. The contrastive learning framework. Simply put, manipulations applied to one image should result in more similar encodings than the encodings of two manipulations of separate images. Something is more self-similar than similar to something else, regardless of transformation. We can map this neatly into the histopathology slide tiles scenario: croppings or rotations of each tile are more similar than to any other tile. By training with this criterion, you get a learned dimensionality reduction, which you can use to great effect. Image adapted from [here](https://blog.salesforceairesearch.com/prototypical-contrastive-learning-pushing-the-frontiers-of-unsupervised-learning/)  |

Contrastive learning works by making an encoder and a decoder: simply compress the image croppings and decompress them, reconstructing them as best as possible. This corresponds to a learned dimensionality reduction, learning the (connected set of) data manifold(s) (if that scared you, see [this video](https://youtu.be/evGm6IJKrDI?feature=shared&t=2209),  [this paper](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=6472238), or [this excellent blog post on VAEs and the representations they learn](https://towardsdatascience.com/understanding-variational-autoencoders-vaes-f70510919f73)). The goal now is to make the compressed representations of different transformations of the same patch be closer to each other than to those of other patches. No labels required!

## Stapling together feature maps for fun and profit (and science)
Now the nice thing is that you might learn to encode image patches of, say, 1,024 by 1,024 = 1,048,576 pixel values each for the RGB channels in only 1,000 dimensions. So you train this model on all these tiles of all your samples, irrespective of the label. Now there are 96 tiles in our original pathology slide above. You could encode those in only 96,000 features, rather than the original 1,024\*1,024\*3\*96 = 301,989,888 features. Nifty! This reduction means we can now staple all the tile representations back together again, into a 1,000*96 matrix, which actually fits on our GPUs for training ML models. So: we’ve trained a fancy dimensionality reductor using contrastive learning, we can compress the individual patches down into a manageable format, and now have features of the whole slide (the top-level object) available for classification!  
Then, a second model can learn to do the actual prediction. That second model can learn how different parts of the image relate: it has features of the whole image available. As well, the ground truth labels are now also in the right format: the 96,000 features do correspond to the top-level label, we need but learn how. It is not so that the tile-level classification has a lot of ‘wrong’ labels, since not each tile of the cancer slide image actually has cancer, or even any material at all. Finally, there is no need for arbitrary (human-defined) aggregation rules. We can let the model figure out the best way to classify, as we usually do in ML and specifically deep learning.

## Conclusion 
In general, this talk ties nicely into the emergence of self-supervised pre-training as a hugely influential paradigm. Here, sheer histopathology slide size forces one’s hand and requires cutting into tiles, but that brings drawbacks. With self-supervised representation learning, the tiles can be projected into a learned, lower-dimensional, informative representation. This then allows one to express an image as a _much reduced_ set amount of features, and turns the MIL problem into a classical classification problem. I am currently working in flow cytometry, and an additional problem there is that each patient might have differing numbers of measured cells. However, that’s no biggie in the end: I can subsample cells from each patient to make similar size batches (upsampling for training), represent them using contrastive learning, and simply make a uniform size of $learned_representations * n_samples$ per patient that all patients can adhere to.
