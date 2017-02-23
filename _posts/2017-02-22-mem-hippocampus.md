---
layout: post
title: "Memory: Hippocampus"
date: 2017-02-22
sources: lecture
type: summary
---

## Motivation: Why We Need the Hippocampus to Learn
The cortex [learns](https://cchen23.github.io/blog/2017/02/09/mem-learning-nn) gradually, updating the weights in the neural network little by little as it accumulates evidence about the world. However, we don't always learn through gradual updates. Sometimes we learn from a one-time event, but  model of gradually updating weights in the cortex does not seem to allow for this.
One idea is to just have the cortex learn faster by making bigger updates to weights in the neural network. But this could break the cortex's existing understanding of the world, since a one-time event could overwrite the cortex's existing worldview.
Learning in the hippocampus provides a solution: the brain uses learning in the cortex for gradually accumulating knowledge about the world, and it uses learning in the hippocampus to rapidly learn from one-time events.

## Learning in the Hippocampus
The hippocampus has strong inhibitory interneurons, which make sure that very few neurons are active at once. Because of this, similar stimuli activate different neurons in the hippocampus, which allows the hippocampus to separate similar patterns from each other. Because of this pattern separation, the hippocampus does not have the same vulnerability to rapid weight changes: since there is much less overlap in activated neurons between stimuli, the hippocampus can rapidly adjust weights without worrying about messing up existing representations.
After the hippocampus rapidly learns something it can layer communicate its knowledge to the cortex over a longer period of time, which allows the cortex to gradually learn the information.

## The Hippocampus is Important for Spatial Memory
In terms of places, our memories involve collections of similar stimuli. For example, if we're at different locations in a room, our memory of each location involves a lot of the sample aspects, with small differences. With its ability to perform pattern separation, the hippocampus is therefore a good area to remember (and differentiate between) spatial memories.
