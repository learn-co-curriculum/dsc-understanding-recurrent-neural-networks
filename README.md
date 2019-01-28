
# Understanding Recurrent Neural Networks

## Introduction

In this lesson, we'll learn about a new type of model architecture we haven't seen yet--**_Recurrent Neural Networks_**!

## Objectives

You will be able to:

* Compare and contrast traditional back propagation with back propagation through time
* Demonstrate an understanding of the role time steps play in RNN models

## Data as Time Sequences

The hallmark of Recurrent Neural Networks is that they are used to evaluate **_Sequences_** of data, rather than just individual data points. So what is sequence data, and how do we distinguish it from other kinds of data, so that we know when to reach for an RNN? 

Time series data is a classix example of sequence data. We care about the value over time, and any given point in time can really only be examining relative to the other points of time in  that sequence. For instance, knowing the price of Google stock today doesn't provide enough information for us to classify it as a something we should or shouldn't buy--for that, we would need to examine today's price relative to the previous day(s) price to see if it's going up or down. 

Another great example of sequence data is text. All text data is sequence data by default--a letter only makes sense when it's words are in the proper order--we would lose all information if we made a "Bag of Letters". Words themselves are sequence data, and can be used for all kinds of novel sequence generation tasks. You've probably seen articles in popular culture about people using neural networks to generate novel band names, cookie names, pokemon names, etc. These are always done with Recurrent Neural Networks, because they are a perfect fit for sequence data. For this reason, RNNs excel at NLP tasks, because they can take in text as full sequences of words, from a single sentence up to an entire document or book! Because of this, they do not suffer the same loss of information that comes from a traditional Bag-of-Words vectorization approach. 

<img src='unrolled.gif'>

Let's take a look at the overall structure of a RNN to see how it interacts with this sequence data!

## Basic RNN Architecture

A basic Recurrent Neural Network is just a neural network that passes it's output from a given example back into itself as input for the next example. Intuitively, this approach makes sense--if we want to predict what Google's stock price is going to be 2 days from now, the most important input we can give it is what we think the price will be 1 day from now!

When drawn as a diagram, RNNs are usually represented in an **_Unrolled_** representation, which shows the components at each given time step. The image on the left is a how a RNN is denoted in a diagram "rolled up", while the image on the right is "unrolled". The current timestep is denoted with the input node $X_t$, which makes the previous time step $X_{t-1}$ and the next time step $X_{t+1}$.  $H_0$ represents the model's output for timestep 0, which will then be passed back into the model in $X_1$. 

<img src='RNN-unrolled.png'>



## Backpropagation Through Time

One interesting aspect of working with RNNs is that they use a modified form of back propagation called **_Back Propagation Through Time (BPTT)_**. Because the model is trained on sequence data, it has the potential to be right or wrong at every point in that sequence. This means that we need to adjust the model's weights at each time point to effectively learn from sequence data. Because the model starts at the most recent output, and then works backwards to calculate the loss and update the weights at each time step, the model is said to be going "back in time" to learn.  Since we have to update the every single weight at every single time step, that means that BPTT is much more computationally expensive than traditional back propagation. For instance, if a single data point is a sequence with 1000 time steps, then our model will perform a full round of back propagation for each of the 1000 points in that single sequence. 

### Truncated Back Prop Through Time

This was a major hurdle for traditional RNN architectures, but a solution exists in the form of the **_Truncated Back Propagation Through Time (TBPTT)_** algorithm! We don't need to go to deep into specifics, but essentially, this algorithm increases performance by breaking a big sequence of 1000 into 50 sequences of 20. This significantly improves training time over regular BPTT, but is still significantly slower than vanilla back propagation. 

Fun Fact: Truncated Back Prop Through Time was invented in the dissertation of Ilya Sutskever, one of the lead researchers at Open AI!



## Summary

In this lesson, we learned about the sequence data. We also learned about the architecture of RNNs, and the modified back prop algorithm they use for training!
