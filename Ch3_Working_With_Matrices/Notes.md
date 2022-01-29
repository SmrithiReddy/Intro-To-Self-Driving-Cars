# Chapter 3: Working with Matrices

## Chapter Overview

1. Introduction to Kalman Filters:
    A kalman filter is an algorithm which uses noisy sensor measurements (and Bayes' Rule) to produce `reliable` estimates of `unkown` quantities

2. State
    The quantities you need to keep track of when programming a car to driive itself

## Lesson 2: Introduction to Kalman Fiters

### Tracking

Tracking the location of other vehicles, pedestrian and predicting the speed of motion is important for a self driving car to avoid collision. 

Kalman Filter is a very popular technique to estimating the state of a system

Kalman filters estimate a continuous state and are uni-modal distribution. 

Similar to Monte Carlo Localization - but is forced to use discrete states and is multimodal distribution

Another popular techniwue is Particle Filter which is both continuous and multi-modal distribution. 

Theses techniques can be used for both Localization and tracking. 

**Kalman Filters**
In kalman filters, the dritribution of a continuous space is given by a Gaussian. A gaussian is a continuous function over the space locations and the area underneath sums up to 1. 

The gaussian is characterized by 2 paramenters, 1. The mean $\mu$ and 2. the width of the gaussian, called the variance and is represented as $\sigma^{2}$

1-D Guassian: Characterized by a $\mu$ and $\sigma^{2}$. So instead os esimating the function as a histogram, in Kalman filters we need to maintains a $\mu$ and $\sigma^{2}$ that is our best estimate of the location of the object we are trying to find. 

$f(x) = \Large1/sqrt(2.pi.\sigma^{2}) . e^{-(x-\mu)^{2}/(2.\sigma^{2})}$

The constant i.e is mutiplied to the exponential is used for normalizing the distribution. 
The $2.\sigma^{2}$ in the denominator of the exponent is also used to normalize the $(X-\mu)^2$. So the larger the difference, the larger the variance. That is , the vairance is a measure of uncertainity. Larger the  $\sigma^{2}$, the more uncertain we are about the actual state. 

Uni-modal means single peak. The guassian is a uni-modal function. 

### Gaussian Summary
- $f(x) = \Large1/sqrt(2.pi.\sigma^{2}) . e^{-(x-\mu)^{2}/(2.\sigma^{2})}$
- unimodal and symmetric
- keeping track of \mu and \sigma to figure out the best estimate 
- using it as a belief in kalman filter. 


### Kalman Filter Measurement and motion
KF represents all measurements by guassians. The kalman filter iterates over 1. Measurement Updates and 2. Motion Updates (called prediction) in a loop 

From previous lass - measurement involves updating our belief and renormalizing the data. Motion meant keeping trach of where all the probability "went" when we moved (which meant using the law of total probability)  

- For measurement update, bayes' rule is used.
- For prediction - total probaility(convolution) is used

Let's say we have an inital guassian with a very large variance and a new measurement about the localization of the vehicle. 

![Tracking: Shifting the mean](https://github.com/SmrithiReddy/Intro-To-Self-Driving-Cars/blob/main/Ch3_Working_With_Matrices/lesson2/kalman_filter_posterior_estimation.PNG)