# Chapter 1: Orientation
## Lesson 4 Notes
### 4.1 Temperatures Affect on Distance Calculation (Tire Volume)
*Tire's change volume and hence the overall circumference based on the temperature. This often gives an inaccurate calculation of the distance measured. One way to mitigate this is through calibration:

Example:

	1. Measure the distance between herself and an object directly behind her.
	2. Turn her wheels exactly one full rotation.
	3. Make the same distance measurement again.
	4. Use the measurements from 1 and 3 to calculate the distance traveled. This is the current circumference of her tires.

**Challenge: Changing Tire Size**

```
from math import pi
def get_tire_diameter(dist_before_turn, dist_after_turn):
    
    # TODO - there's a bug in this function! Find and fix it!
    
    circumference = dist_after_turn - dist_before_turn
    diameter = circumference / pi
    return diameter
```

### 4.2 Lateral Acceleration of a Car
Lateral Acceleration is the sideways acceleration of the car perpendicular to its velocity vector. 

* Usually calculated as a 'g' force. 
* $a_{lat} =\frac{v^2}{R}$

**Challange: Planning**
In junkyard conditions, the maximum lateral acceleration that Carla's tires can support is $12 m/s^2$. If she's traveling at a velocity of $30 m/s$, what's the sharpest turn (minimum turning radius) she can make?

*$R = 30^2/12 = 75m$*

### 4.3  Choosing an Optimal Solution (Shortest Path Example)

```
# Right now the make_decision function ALWAYS decides to go left.
# Modify this function so it behaves appropriately.

def make_decision(L1, L2, L3, L4):
    if (L1+L2)<=(L3+L4):
        return "R"
    else: return "L"


##########################################################
# 
# The code below is similar to the code that Udacity
# will use to test the correctness of your submission.
# You don't need to modify it but it may
# be helpful to look at for Python syntax help
# 
def test_make_decision():
    # start by initializing this to 0
    number_correct = 0
    
    # TEST 1, should return "R" since right path has 
    # length 5 which is < left path with length 8
    length_1 = 2
    length_2 = 3
    length_3 = 4
    length_4 = 4
    
    decision = make_decision(length_1, length_2, length_3, length_4)
    
    if decision == "R":
        # Test 1 passes
        number_correct = number_correct + 1
        
    # TEST 2, should return "L" since right path still 
    # has length 5 but left is only 3.
    length_3 = 1
    length_4 = 2
    
    decision = make_decision(length_1, length_2, length_3, length_4)
    if decision == "L":
        # Test 2 passes
        number_correct = number_correct + 1
    
    if number_correct == 2:
        all_correct = True
    else:
        all_correct = False
    
    return all_correct
    
if test_make_decision():
    print("Nice work! Your function passed both test cases.")
else:
    print("Not quite. Your function didn't pass both test cases.")
```


    
