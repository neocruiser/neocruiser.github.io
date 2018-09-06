---
layout: post
title: "Is reinforcement learning suitable for cancer predictions?"
date: 2018-09-06 14:51:02
categories: [genetics, pipelines]
tags: [machine learning, genetics]
---

`Reinforcement learning` is another statistical beast that has a special analytical design because of which it can recognize special patterns in the data.
To deliver a prediction it requires first a feedback, then an input. 
It will train the user options, which are pushed onto the execution stack, then produces an outcome.
Lastly, relying on an action and a judgement will help the model converge on a single prediction.

* The world can be cancer.
* A state (feedback and input) can be cell growth or cell cycle.
* An option can be mutation or copy number variants.
* A reward (action and judgement) can be synonymous or deleterious mutations.
  - Low reward is for an outcome being cancer
  - High reward is for either outcomes, dead cell or healthy cell
* A policy (good/bad mutation) maps observations (mutations) to actions (consequence having that mutation).


Because of its flexibility, RL is vulnerable to environment overfitting.
However, predicting the distribution, helps the agent (trained model) get an idea about the state of the environment (world).
From that distribution, an expectation score is estimated.
The score helps the agent learn.
Therefore, from the agent's perspective, the prediction is best when the whole distribution is known.


![Notes on reinforcement learning](/assets/2018/reinforcement-learning-cancer.jpg){:height="560px" width="420px"}



[arxiv]:https://arxiv.org/search/?query=deep+learning&searchtype=all&source=header