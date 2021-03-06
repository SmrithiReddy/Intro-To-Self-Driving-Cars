# Capter 2: Bayesian Thinking
## Lesson 1: Introduction
**Course Overview**
1. Joy Ride
2. Probability
3. Conditional Probability
4. Programming Probability in Python
5. Bayes' Rule
6. Programming Bayes' Rule and World Representations
7. Robot Localization
8. Histogram Filter in Python (project)

## Lesson 2: JoyRide
**Joy Ride - Project Overview**

This is a quick, simple project that gives you a chance to write code that controls a simulated car as you get familiar with the Workspaces you'll be using throughout this Nanodegree program. This project has three parts (but you will only submit part three).

**Part One - Drag Race:** In this part, you'll write code that lets a car jump over a grove of trees. This might not be a common scenario for a self-driving car, but it will get you familiar with the programming interface.

**Part Two - Circular Track:** In this part, you'll write code that lets a car navigate a circular track. In doing so you'll explore the relationship between steering angle and turning radius.

**Part Three - Parallel Park:** In this part, you'll write a sequence of instructions that successfully parallel parks a car. In a real car, you obviously wouldn't be able to try repeatedly and hit other cars while you perfect your parking, but in this project, you can try as many times as you need to!

"*Tip:* For Part Three, the simulator contains a little bit of noise each time you launch it. To help account for this, consider spending a second or two of time traveling slowly forward in the simulator before reversing into your parallel parking. You should also consider using a fairly low vehicle velocity at all times."

*Note:* The project files are in the Lesson 2 Folder.

## Lesson 3: Probability ##
### Probability ###
Probability and Statistics have an opposite relationship.
- In Statistics, given `data` we infer the `causes`
- In Probability, given `causes` we infer the `data`

Basic Law of Probability: P(A) = 1 - P(~A)

### Managing the Probabilistic Complexity ###
Roboticists will often use the term state space to describe the set of all possible outcomes for a probabilistic event.

For a coin the state space for a "flip" event can be written mathematically as:

{H,T}

And for a car at an intersection the state space for a "turn" event can be written mathematically as:

{L,S,R}

Coins and cars may seem differently, but we can treat them in similar ways when we think in terms of events and state spaces.

In the last question you saw that calculating a truth table for 2 coin flips requires 4 calculations while calculating the truth table for 2 car turns at an intersection requires 9 calculations.

We can make these statements more broadly applicable:

When calculating the truth table for 2 events which each have a state space size of 2, we need to make 4 calculations.

When calculating the truth table for 2 events which each have a state space size of 3, we need to make 9 calculations.

And in fact, there's a mathematical pattern here that can be expressed algebraically:

When calculating the truth table for N events which each have a state space size of x, we need to make $x^N$ calculations. 

N gets very big very fast as x or N get bigger.

You will see later this Nanodegree how this exponential complexity growth can really slow down the performance of the code running inside of a self driving car.

- Probability of Event = P
- Probability of Opposite Event = 1-P
- Probability of Composite Event for independent events = PxP..P

### Probability Concepts for independednt events ###
Probability can typically be thought of as:

$\Large \frac {\textrm {Number of ways an event can occur}}{\textrm{Total number of events that could occur}}$???
 
An "event" is defined as some type of state that can happen. For example, turning "left" or "right" are both events. Similarly, pressing the "gas" or "brake" are also events. All probabilities will be between 0 and 1 inclusive.

Often, the notation P(X) is used. This typically means the probability of "X" occuring.

1. Adding Probabilities
    OR => sum probabilities
2. Compliments:
    
     Often in probability, there will be a time when you want to know the result of a specific event. Unfortunately, sometimes, this event can be really tricky to calculate. However, it may be really easy to calculate all other events except this event. By doing this, we can exploit the following property:

    $\textrm {Specific outcome = 1 - (The sum of probability of all other events)}$

3. Multiplying Probabilities -
    AND => Multiply Probabilities

## Lesson 4 ##
### Conditional Probability ###

Conditional probability is defined as the `likelihood of an event or outcome occurring`, based on the occurrence of a previous event or outcome. Conditional probability is calculated by multiplying the probability of the preceding event by the updated probability of the succeeding, or conditional, event.

**Notation Note**

|Symbol     | Usage     | Interpretation    |

|-----      |:----  :| ---:|

P   |P(A)	| "The probability of event A occurring" |

|$\lnot$	| $P(\lnot A)$ |    "The probability of event A not occurring" |

|$\mid $  |	$P(A \mid B)$ |	"The probability of event AA occurring given that event BB occurs"|

- Consider A is an independent Event and X is a an event dependent on A
### Concept and Formulae ###

**1. Total Probability**: P( X ) = P( A ) * P( X | A ) + P($\lnot$ A) * P( X | $\lnot$ A)

**2. P(A and B)**

let???s calculate the conditional probability of some events. In order to do this we need the following formula:

$P(A|B) = P(A \cap B) / P(B)$

What this means in English is given an event B, find all the events shared with A, and divide by the probability of event B happening by itself. The \cap??? symbol for intersection represents these events shared between A & B.

When dealing with these probabilities, the basic rules of algebra apply so we manipulate the equation by multiplying both sides by P(B) to also look like this:

$P(A \cap B) = P(A|B) * P(B)$

**3. Law of Total Probability**

A useful law when dealing with conditional probability is the Law of Total Probability.

If $B_1, B_2, B_3, ...$ is a partition of a sample space S, then for any event A:

$P(A)=\sum_i P(A \cap B_i) = \sum_i P(A | B_i) * P(B_i)P(A)$

The formal definition is a bit "mathy", but think of it as calculating the sum of all probabilities necessary to ensure all scenarios for specified event are included. This is actually quite similar to the equation from before, but now we calculate it for each i of B, and then sum all of these together.

## Lesson 5: Programming Probability in Python ##

Useful Libraries (Modules):
1. random - Used to generate random values

### Simulating Coin Flip ###
```

# Import the random module and reference it as rd
import random as rd

def simulate_coin_flips(num_trials):
    '''
    A function to simulate coin flips
    
    Args:
        num_trials (int): The number of coin flip 
                          trials to simulate
    Returns:
        int: The percentage of heads from the trials
    '''
    heads = 0 # A counter for the number of heads
    tails = 0 # A counter for the number of tails
    p_heads = 0.5 # The probability for heads

    # Simulate coin flips up to the num_trials specified
    for i in range(num_trials):
        # Collect a random number between [0,1]
        random_number = rd.random()
        # If the number is less than heads count it as heads
        # Otherwise, count it as tails
        if random_number < p_heads:
            heads = heads + 1
        else:
            tails += 1
    # Calculate the percentage of heads based on the number of 
    # heads and trials
    percent_heads = heads / num_trials
    return percent_heads
    
percentage = simulate_coin_flips(200) # calling the function
print(percentage)# Import the random module and reference it as rd

```

### Simulating Dice Rolls and Basic Visualization ###

```

# Import the random module and reference it as rd
import random as rd


def simulate_dice_rolls(N):
    """
    Simulates dice rolls
    
    Args:
        N (int): The number of trials
        
    Returns:
        list: roll counts [1,6]
    """
    # Create a list to track the 6 options for the roll
    roll_counts = [0,0,0,0,0,0]
    for i in range(N):
        # Randomly select a value from the list (1 to 6)
        roll = rd.choice([1,2,3,4,5,6]) 
        # Recall indices start at 0 so we need to decrement
        index = roll - 1
        roll_counts[index] = roll_counts[index] + 1
    return roll_counts

def show_roll_data(roll_counts):
    """
    Shows the dice roll data
    
    Args:
        roll_counts (list): The roll counts stored in the list
        
    Returns:
        list: roll counts [1,6]
    """ 
    # Gets the number of sides of the dice and prints
    # the side of the die. 
    # enumerate creates the position of the die and the
    # list value
    for dice_side, frequency in enumerate(roll_counts):
        print(dice_side + 1, "was rolled", frequency, "times")
        
roll_data = simulate_dice_rolls(1000)
show_roll_data(roll_data)
```

## Lesson 6: Bayes' Rule ##

### Bayes' Rule in Robotics ###
Given an initial prediction if we are given additional related data that the initial prediction depends on, we can improve the prediction. 

Example: Given a low accuracy GPS Signal - by collecting additional data about the surroundings using sensors, we will be able to predict our current location more accurately

### Learning from Sensor Data ###

**Sensors:**

**GPS:**  Location estimate of the vehicle on a map - Low accuracy 

Self-driving cars mainly use three types of sensors to observe the world:

1. **Camera**, which records video,

2. **Lidar**, which is a light-based sensor, and

3. **Radar**, which uses radio waves.

All of these sensors detect surrounding objects and scenery.

Autonomous cars also have lots of internal sensors that measure things like the speed and direction of the car's movement, the orientation of its wheels, and even the internal temperature of the car!; 

### Baye's Rule ###
# Foluma: #
$P(A|B) = \Large\frac{P(B|A).P(A)}{P(B)} $
**Conditional Probability Terms** 

***1. Prior Probability (Source: Wikipedia)***

In Bayesian statistical inference, a prior probability distribution, often simply called the prior, of an uncertain quantity is the probability distribution that would express one's beliefs about this quantity before some evidence is taken into account.

For example: Knowing that a car stopping at an intersection (P(S)) and the presence of a yellow traffic light (P(Y)) are related events, and are known as `Prior Probability`

***2. Sensitivity (True Positive Rate)[Source: Wikipedia]***

Refers to the probability of a positive test, conditioned on truly having the condition (or tested positive by the `Gold Standard test` if the true condition can not be known).

*Example:*
 Probability of geitting Tested Positive, given that you have Cancer. i.e P(P|C)


***3. Specificity (True Negative Rate) [Source: Wikipedia]***
 
 Refers to the probability of a negative test, provided one does not have the condition (judged negative by the `Gold Standard`).

*Example:*
 Probability of geitting Tested Negative, given that you dont have Cancer. i.e $P(N|\lnot C)$

### Prior and Posterial Probability ###

Bayes' Rule incorporates the test evidance with prio probability to give a posterior probability

P(Pos, C) = P(Pos|C) P(C)

P(Neg, C) = P(Neg|C) P(C)

P(Pos, ~C) = P(Pos|~C) P(~C)

P(Neg, ~C) = P(Neg|~C) P(~C)

### Baye's Rule Example Walkthrough ###
**Prior Probabilities**

The robot is perfectly ignorant about where it is, so prior probabilities are as follows:

P(at red)=0.5

P(at green)=0.5

**Conditional Probabilities**
The robot's sensors are not perfect. Just because the robot sees red does not mean the robot is at red.

P(see red???at red)=0.8

P(see green???at green)=0.8

**Posterior Probabilities**
From these prior and posterior probabilities we are asked to calculate the following posterior probabilities after the robot sees red:

P(at red???see red)

P(at green???see red)

and as a reminder, Bayes' rule looks like this:

$ P(A|B) = \Large\frac{P(B|A) \cdot P(A)}{P(B)}$ 
 

or, if we want to use our "versions" of A and B (for posterior #1)...

$P(\text{at red}|\text{see red} ) = \Large\frac{P(\text{see red}|\text{at red}) \cdot P(\text{at red})}{P(\text{see red})}$
 

Now, we can read two of those terms from what we already know about our prior and conditional probabilities which means we can rewrite this as...

$P(\text{at red}|\text{see red} ) = \Large\frac{0.8 \cdot 0.5}{P(\text{see red})}$ 

But we still have one unknown! What was the probability that we would see red? The answer is 0.5 and there are two ways I can convince myself of that. The first is intuitive and the second is mathematical.

Why is P(see red) 0.5?

*Argument 1: Intuitive*

Of course it's 0.5! What else could it be? The robot had a 50% belief that it was in red and a 50% belief that it was in green. Sure, its sensors are unreliable but that unreliability is symmetric and not biased towards mistakenly seeing either color.

So whatever the probability of seeing red is, that will also be the probability of seeing green. Since these two colors are the only possible colors the probability MUST be 50% for each!

*Argument 2: Mathematical (Law of Total Probability)*

There are exactly two situations where the robot would see red.

When the robot is in a red square and its sensors work correctly.
When the robot is in a green square and its sensors make a mistake.
I just need to add up these two probabilities to get the total probability of seeing red.

$P(\text{see red} ) = P(\text{at red}) \cdot P(\text{see red} | \text{at red}) + P(\text{at green}) \cdot P(\text{see red} | \text{at green})$

I can read these quantities from above!

$P(\text{see red} ) = 0.5 \cdot 0.8 + 0.5 \cdot 0.2$

$P(\text{see red} ) = 0.4 + 0.1$

$P(\text{see red} ) = 0.5$

## Lesson 7: Programming Bayes Rule and World Representations ##

### 1. Bayes Rule Steps (Review) ###

Before we dive into code that utilizes Bayes' rule, let's review what we've learned in the previous lesson.

We've seen that Bayes' rule allows us to improve a prior probability by incorporating new evidence (from observed data or tests) and forming a new posterior probability. It does this through a series of mathematical steps.

To describe the steps, I'll be using the notation HH for hypothesis (ex. the likelihood that a car is in a certain location or that a person has cancer, etc.), and T for observed test/sensor data (ex. a car sees the color green or a positive medical test result is returned). For example, $P(T|\neg H)$ is the probability of sensor reading occurring given that the hypothesis has not occurred.

**A note on notation**

As you work through these problems, you may see other notation, P(H???T), or P(X|U), or P(A|B) (and so on) where one letter indicates a hypothesis and the other indicates observed data. Different notation; same concept, and as long as you are familiar with the concept, you should be well equipped to deal with changing notation!

1. Prior probabilities

    The first step in Bayes' rule is to determine any prior probabilities. Ask yourself, based on previous data, how likely is a hypothesis, or specific event, H to happen?

    Determine P(H)

    Once you have P(H), you can derive $P(\neg H)$

2. Conditional/test probabilities
    You should also know, through sensor or test data collection, how likely a certain test or sensor reading is to occur given that the hypothesis H has or has not occurred.

    Determine P(T|H) and $P(T|\neg H)$

    Once you have P(T|H)P(T???H), you can derive P(\neg T|H)P(??T???H)
    Steps 1 and 2 give you all the information you need to perform Bayes' rule, and form a prediction about how likely a hypothesis is to be true given certain observed, related data.

3. Joint Probabilities

    The next step is to calculate the four joint probabilities of the prior and the test probabilities. Two examples are given below.

    $P(T, H) = P(T|H)\cdot P(H)$

    Likewise, $P(T, \neg H) = P(T|\neg H)\cdot P(\neg H)$

4. Total probabilities

    You'll then need to determine the total probability of a test result or sensor reading, so that you can use this value to normalize the posterior probability (which is the last step of Bayes' rule. The total probability of a test result is the sum of the joint probabilities in which that test result occurs. An example is given below.

    $P(T) = P(T, H) + P(T, \neg H)$
5. Posterior probability (last step)

    The last step is to determine the probability of an event given a sensor reading or certain test data. And this is given by Bayes' rule. An example is shown below.

    $P(H|T) = \Large\frac{P(T|H)\cdot P(H)}{P(T)}$
???
## Lesson 8: Probability Distribution ##
### 1. What is probability Distribution ###
Probability distributions allow you to represent the probability of an event using a mathematical equation. Like any mathematical equation:

- probability distributions can be visualized using a graph especially in 2-dimensional cases.

- probability distributions can be worked with using algebra, linear algebra and calculus.

These distributions make it much easier to understand and summarize the probability of a system whether that system be a coin flip experiment or the location of a self-driving car.

**Types of Probability Distribution**
1. discrete probability distributions
    - the y- axis represents the probability of an event occuring. 
    - the x axis takes on discrete values
2. continuous probability distributions
    - the y-axis represents the probability density function
    - the x axis takes on any real value in the range [ $-\infty, \infty$]

- the x axis in both the cases represents the main variable of interest

![Probability Distribution Image](https://github.com/SmrithiReddy/Intro-To-Self-Driving-Cars/blob/main/Ch2_Bayesian_Thinking/lesson8/probability-distributions.jpg)

### 2. Discrete vs Continuous Variables ###
**Discrete Distribution**
A few interesting characteristics about discrete probability distributions:

- For all values on the x-axis, the y value is greater than or equal to 0.
- For each x, the probability p(x) is equal to the y value
- The sum of all y values is 1; there's a 100% chance that something will occur.

Here is what we mean by the sum of all y values is 1. When flipping a coin three times, there is a 100% chance that you will either get zero heads, 1 heads, 2 heads or 3 heads (ignoring the very very small chance that the coin lands on its side).

**Continuous Distribution**
The continuous distribution has an un-broken line across the entire x-axis range. You could have a velocity of 20 or 20.5 or -10.451.

 y-axis label on the continuous distribution is the: "probability density function". For the discrete probability distribution, the y-axis represented the probability of an event occurring. In the continuous case, the probability density function does not represent probability directly; instead, `the area underneath the density function curve represents probability`.

 **Characteristics of a Continuous Distribution**
- The y values must be greater than or equal to 0.
- The probability of a specific x value occurring is equal to 0
- The probability of an event occurring between two values of x is equal to the area under the curve between those two x values.
- The total area under the probability density function curve is equal to 1.
- f(x)(y-axis) need not be continuous.
- f(x) i.e probability density function can be greater than 1. 

In practice, these rules mean that the probability that velocity equals exactly 20 is zero. For a continuous distribution, you can only calculate a probability between a range of values like 19.99 and 20.01.
Because the total area under the curve is 1, there is a 100% chance that the velocity has some value between negative infinity and positive infinity.

There are many different types of continuous distributions: [link to list of continuous probability distributions](https://en.wikipedia.org/wiki/List_of_probability_distributions#Continuous_distributions).

To calculate probabilities with a continuous distribution, you have to calculate the area underneath a curve. Calculating the area under a curve like in the above visualization requires calculus or a software program.

**Uniform Continuous Distribution**
The uniform continuous distribution forms a rectangle. 

Therefore, Area under the curve = base * height
![uniform continuous distribution](https://github.com/SmrithiReddy/Intro-To-Self-Driving-Cars/blob/main/Ch2_Bayesian_Thinking/lesson8/uniform-continuous.png)

### Probability Distribution in Robotics ###
In the nanodegree, you are going to see robot probability distributions represented two different ways:

1. with discrete probability distributions
2. and with continuous probability distributions

Discrete probability distributions are used when you track a robot's movement across a map divided into square grids. Each grid is a discrete location where the robot could be located.

## Lesson 10: Gaussian Distribution ##
When modeling uncertainty in a sensor measurement, you'll use a Gaussian distribution. The uncertainty in a sensor measurement or the location of a pedestrian, for example, is oftentimes modelled with a Gaussian distribution.

**Terms:**
- **population** refers to the entire set of all data points. Like if you were measuring people's weights, then the population would be all people in the world.
- **sample** refers to a part of the population. In the weights example, you might take a random sample of the population since it would be practically impossible to measure the weights of all humans.
- **mean** is the average value, which in this case would be the average weight of all humans.
- **standard** deviation measures the spread in the data. Does the data tend to hover around the mean, or is the data more spread out?

[Useful link for a referesher/review](https://stattrek.com/sampling/populations-and-samples.aspx)

### 1. Gaussian Distribution ###

![Gaussian distribution](https://github.com/SmrithiReddy/Intro-To-Self-Driving-Cars/blob/main/Ch2_Bayesian_Thinking/lesson10/gaussian2.png)

You might recognize this shape; it's oftentimes called a bell-shaped curve. Notice that the y-axis says "probability density function" just like the uniform continuous distribution.

The x-axis currently says "x-value"; however, the x-axis could take on any continuous variable like temperature, height, or velocity.

**Gaussian Equation**
Here is the probability density function for the Gaussian distribution:

$f(x) = \Large \frac{1}{\sqrt{2\pi \sigma^{2}}} e^{\frac{-(x-\mu)^{2}}{2\sigma^{2}}}$

**Input Variables:**
- $\mu$ : Mean : represents population mean
- $\sigma$ : Standard Deviation : Represents the spread
- x : input variable

the mean and standard deviation are constants when dealing with a population. So for a specific population, the only value that varies is x.

- As the mean increases while keeping the data and standard seviation constant - the curve shifts to the right
- As the standard deviation increases, keeping everything else constant - the curve becomes wider and flatter. As the standard deviation increases, uncertainty increases as well. 

Consider an example of the temperatures in San Francisco. Assume that the minimum daily temperature follows a Gaussian distribution.Say that on average, the minimum winter temperature in San Francisco is 50 degrees Fahrenheit. In other words, If you measured the minimum temperature every day of winter over all winters ever, the average value would be 50. Let's say the standard deviation is 10 degrees.

**Changing Mean Visualization:** 

![Gaussian distribution Average is 40](https://github.com/SmrithiReddy/Intro-To-Self-Driving-Cars/blob/main/Ch2_Bayesian_Thinking/lesson10/gaussian40.png)

![Gaussian distribution Average is 50](https://github.com/SmrithiReddy/Intro-To-Self-Driving-Cars/blob/main/Ch2_Bayesian_Thinking/lesson10/gaussian50.png)

![Gaussian distribution Average is 60](https://github.com/SmrithiReddy/Intro-To-Self-Driving-Cars/blob/main/Ch2_Bayesian_Thinking/lesson10/gaussian60.png)

**Changing Standard Deviation(SD) Visualization:**

![Gaussian distribution SD is 5](https://github.com/SmrithiReddy/Intro-To-Self-Driving-Cars/blob/main/Ch2_Bayesian_Thinking/lesson10/gaussian5.png)

![Gaussian distribution SD is 10](https://github.com/SmrithiReddy/Intro-To-Self-Driving-Cars/blob/main/Ch2_Bayesian_Thinking/lesson10/gaussian10.png)

![Gaussian distribution SD is 15](https://github.com/SmrithiReddy/Intro-To-Self-Driving-Cars/blob/main/Ch2_Bayesian_Thinking/lesson10/gaussian15.png)

Keeping the mean at 50 - let's say the standard deviation changes to  the following values: [5, 10, 15]. 

When the standard deviation is five, the distribution looks tall and skinny, which implies that the temperature is more likely to be near 50 degrees.

When the standard deviation increases to 15, the distribution gets flat and wide; the probability that the temperature is near 50 goes down while the probability that the temperature is farther to the left or to the right on the x-axis is increasing.

## Lesson 11: Robot Localization ##

Finding the location of the robot in its environment. 

To stay in lanes - Self driving cars need to know where they are in space to an accuracy of 10cm

We initialize the robot's model current belief about where it might be in the world by a uniform function that assign equal weight to to every possible location in the world - Called the state of maximum confusion (Modeled as Uniform Continuous Distribution). Let's say we have identical markers/doors - and the robot is able to sense these objects (and the object location on the map is known), the probability that the robot is near one of these increases and the likelihood of its present in other areas decreases. (The new prediction made based on a prediction is called `posterior` belief)

![Robot Localization: Belief](https://github.com/SmrithiReddy/Intro-To-Self-Driving-Cars/blob/main/Ch2_Bayesian_Thinking/lesson11/Belief.png)

If the robot is moving right- the probability distribution can shift right, but because its motion is uncertain, the known belief curves flatten as they shift to the right. The process of moving the beliefs to the right side is called a 'convolution'. 

![Robot Localization: Convolution](https://github.com/SmrithiReddy/Intro-To-Self-Driving-Cars/blob/main/Ch2_Bayesian_Thinking/lesson11/Convolution.png)

Let's say, the robot senses the next door. The new belief is multipied by the convoluted belief (now the `prior`) and the robot has localized itself since it is belif wight is focused at one point. 

![Robot Localization: Belief](https://github.com/SmrithiReddy/Intro-To-Self-Driving-Cars/blob/main/Ch2_Bayesian_Thinking/lesson11/TotalProbability.png)

### Uniform Probability ###
It is the equal liklihood of the robot being at any position in space. 

Example: Given a 2D 10x10 grid. The robot can initially be located in any grid with the probability of 1/100. 

### Probability after sense ###
If the world is divided into known object spaces and the robot can sense the environment, the probability of the robots location relative to the known objects increases compared to the rest of the world space. 

Example,
world = ['red', 'green', 'red', 'red', 'green','green']. 

initial_probability = 1/6 at each location. 
R(B) = [1/6, 1/6, 1/6, 1/6, 1/6, 1/6]
If the robot senses a given color then lets say that the probability that it is in that location is 0.6 and that it is in a different location is 0.2. 
=> pHit = 0.6
pMiss = 0.2

then if the robot sees red. the new updated probability of the robots location can be given by:
p[i] * pHit if in cell with correct color
p[i] * pMiss it is in cell with wrong color

=> robots new/updated belief of world R(B') = [0.1,1/30,0.1,0.1,1/30,1/30]

Since the total does not add up to 1 and we want the total probabilty to add up to one (i.e the probability that the robot is somewhere in the world should be 1), we must normalize the distribution

the normalized distribution of updated belief R(B)= R(B'_i)/Sum(R(B')) 

S(R) = 0.8 //accuracy of sense when it detects red
S(G) = 0.5 //accuracy of sense when it detect green

What is the new probability that the  
pHit = 0.8
pMiss = 0.2

### Probability after motion
Lets say that the robot starts moving and takes 'U' steps at a time. 
The location of the robot cannot be predicted accurately in the real world. We can therefore assign probabilities that the robot is that the location that it thinks it has moved to, and to irs surroundings a decreasing probability. 

So lets say the robot takes 2 steps at a time. Let's assign probabilities:
- The probability that it moves exactly 2 steps : $P(X_{i+2} = 0.8)$
- Probability of undershoot by 1 step: $P(X_{i+1} = 0.1)$
- Probability of overshoot by 1 step: $P(X_{i+3} = 0.1)$

Notice that the probabilities add up to 1. 

Given that the robot is at a location in a 6 position grid i.e p = [0,1,0,0,0],
(Assume that the world is cyclic) 

If the robot moves by 2 positions. what is the new updated probability given the above information:
p_new = [0,0,0.1,0.8,0.1]

With the assumption that the world is cyclic, if the robot keeps moving 2 steps at a time, the likelihood that the robot is at any given location keeps reducing until the probability distribution over the cells becomes a uniform probability distribution. The distribution with absolute least information is Uniform Probability Distribution

i.e the robots probability of being in any cell cannot be lower that the equal likelihood estimation. 
"Limit (or Stationary) Distribution" if we continue the motion is [1/6, 1/6, 1/6, 1/6, 1/6, 1/6] 

This is ralated to the "balance property", according to which in our example considering location 4: P(X_4) = 0.1 * P(X_3) + 0.8 * P(X_2) + 0.1 * P(X_1)

this simply means that the robot can reach the location X_4 from X_1, X_2 or X_3. The probability of reaching X_4 from a previous time step is therefore the sum of the products of probability of being in a certain location and probability of motion from that location to the new location. 

### Robot Localization
The robot's localization in the world can be thought about as the robot's initial belief of its location in the world being updated based on the sense and move cycle. 
- When the robot senses its surrounding - it gains information i.e its entropy decreses
- When it moves - it loses information (Convolution) - i.e it's entropy increases

**Entropy** represents the amount of uncertainity in a system. The maximum uncertainity occurs when all the positions have equal probabilities. 

Measure of information that the distribution has
$ Entropy = \Sigma(-p \times log(p)) $

### Sense and Move Code Example ###
```
p=[0.2, 0.2, 0.2, 0.2, 0.2]
world=['green', 'red', 'red', 'green', 'green']
measurements = ['red', 'red']
motions = [1,1]
pHit = 0.6
pMiss = 0.2
pExact = 0.8
pOvershoot = 0.1
pUndershoot = 0.1

def sense(p, Z):
    q=[]
    for i in range(len(p)):
        hit = (Z == world[i])
        q.append(p[i] * (hit * pHit + (1-hit) * pMiss))
    s = sum(q)
    for i in range(len(q)):
        q[i] = q[i] / s
    return q

def move(p, U):
    q = []
    for i in range(len(p)):
        s = pExact * p[(i-U) % len(p)]
        s = s + pOvershoot * p[(i-U-1) % len(p)]
        s = s + pUndershoot * p[(i-U+1) % len(p)]
        q.append(s)
    return q

for k in range(len(measurements)):
    p = sense(p, measurements[k])
    p = move(p, motions[k])
    
print p     

```

### Localization Summary ###

- The robot maintains a function of all possible places where a road might be.
        Belief = Probability
- Measuremnt Update. 
        Sense = Product of prbabilities followed by Normalization
- Motion Update 
        Move = Convolution = (Addidion of Reverse Engineered probabilities)

### Histogram Filters

Histogram filters decompose the state space into finitely many regions and represent the cumulative posterior for each region by a single probability value. When applied to finite spaces, they are called discrete Bayes filters; when applied to continuous spaces, they are known as histogram filters.


Histogram Filters: 
A Markov model is a model where the world was divided into discrete grids, and each grid was assigned a probability. 

        -       -        -       -      -
        0.2     0.1     0.5     0.1     0.2

Such a representation of probability over spaces is called a histogram. It divides the continuous space into discrete finite grid cells and estimated the posterior distribution by a histogram over the original distribution. The histogram is a mere approximation for the continuous distribution

The y axis is the probability and the x axis is the bins (space block)

(Also called Monte Carlo Localization)