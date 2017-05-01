---
layout: post
title: "Memory: Eyewitness Testimony and Discriminability"
date: 2017-05-01
sources: lecture
type: summary
---

## Discriminability and ROC Curves

A memory for something we've seen before tends to be stronger, while a memory for something new tends to be weaker. We can model memory strengths with probability distributions, in which memory strengths for repeated stimuli tend to be higher and those for new stimuli tend to be lower. ![signal detection](https://www.researchgate.net/profile/John_Wixted/publication/5897698/figure/fig7/AS:279929028661266@1443751689646/Figure-4-The-signal-detection-interpretation-of-remember-know-judgmentsa-A-strong.png)
Then we can set some threshold memory strength to determine whether a stimulus is new (a "foil") or old (a "target"). If a memory is stronger than this threshold then we classify it as an old memory, and if it is weaker than the threshold, then we classify it as a new memory.

Since the distributions overlap a bit, sometimes we'll mistakenly think we've seen a new item before (a false alarm), while other times we'll mistakenly think we haven't seen an old item before (a miss). Other times, we'll correctly classify an old item as "old" (a hit) or a new item as "new" (a correct rejection). The more separate the distributions, the more accurate our classifications. To compute how easy it is to discriminate between "new" and "old" items, we can generate an ROC curve from the model, which plots hit rates against false alarms. ![ROC curve](https://www.researchgate.net/profile/John_Wixted/publication/5897698/figure/fig2/AS:277623876931587@1443202098222/Figure-2-High-thresholdsignal-detection-theory-and-the-receiver-operating.png). The greater the area under the ROC cuve, the easier it is to distinguish between old and new stimuli.

## Application: Eyewitness Testimony

We can use ROC curves to see how well people can identify someone who committed a crime. In a lineup, eyewitnesses are presented with a series of people and must identify whether they were the perpetrator of a crime. By simulating this situation in controlled studies, experimenters can use ROC curves to see how well eyewitnesses can distinguish between someone they saw commit a crime (the "target") and others added into the lineup (the "foils"). Ideally, the lineups function in a way that encourages the highest hit:false alarm ratio, which can be determined by computing the area under an ROC curve.
Experiments such as these have shown that presenting suspects all at once causes a larger area under the ROC curve than presenting suspects sequentially, possibly because the presentation of multiple similar suspects allow eyewitnesses to determine which characteristics of a suspect are most diagnostic about whether they were the perpetrator of a crime.
