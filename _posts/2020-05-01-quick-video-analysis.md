---
layout: post
title: A Quick and Dirty Way to Count Bees

date: 2020-05-01
description:
author: Josh Haug
tags:

- Bees
- Video
---

<div class="message">
Today we'll explore some basic image processing techniques to count bees. These require <b>no training data</b>, so we'll try them first before moving on to fancier techniques.
</div>

The number of bees in the entrance of the hive is a good indicator of the health of the hive.  NEED CITATION.  

Say I have a video of the entrance of a beehive, like this:
![ ](assets/phone-basic.mp4)

If I wanted to count the number of bees in each frame, I *could* set up and train an object detection CNN.  But if I was lazy, I could collapse the color data and apply a Gaussian blur to each frame, like so:
![ ](assets/phone-blur.mp4)

And I could then apply pixel thresholding to get the dark spots, like so:
![ ](assets/phone-darkspots.mp4)

To interpret the list of points as separate objects, we can use a clustering algorithm.  Here's an example using [hierarchical clustering](https://en.wikipedia.org/wiki/Hierarchical_clustering).

![  ](assets/phone-clusters.mp4)

It **kind of** works!  From here we can count the clusters.

Some clear problems though:

* I had to determine a few values experimentally, like intensity threshold and clustering distance threshold
* This only works because the bees' heads and thoraxes are the darkest things in frame. Any dark black objects on the ground would also be counted as bees.

This technique is fast but not reliably accurate -- it is quite literally "quick and dirty".  But the small amount of computation required makes it suitable for a low-power application (e.g. Arduino running on a battery).  
