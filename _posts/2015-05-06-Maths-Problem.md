---
layout: post
title: Maths Problem
---

# Maths Problem

I recently came across an interesting maths problem, aimed at 12-13year olds. It read...

----------

Each different letter in the following addition sum represents a different digit from 0-9 inclusive (neither P nor T are equal to zero, and not the digits are used)

P Q R D + T U V Q = T U R Q W

Explaining your reasoning carefully, find which letters correspond to which digits.


--------

## The solution




## The python implementation

I felt it would be a good exercise to attempt to solve this problem in python.

The difficult part would be looping through all the possible values for each letter. Fortunately, the built in `itertools` package has an efficient method called `permutations` that lent itself nicely to solving the problem.

From here the solution was simple

```python

import itertools

for perm in itertools.permutations(range(0,10),8):
		
	[P,Q,R,S,T,U,V,W] = perm

	if 10**3*(P+T-U) + 10**2*(Q+U-R) + 10**4*(-T) + 10*(R+V-Q)
		+ (S+Q-W) == 0 and P*T != 0:
		
		print
		print 'Result'
		print ' ' + str(P) + str(Q) + str(R) + str(S)
		print '+' + str(T) + str(U) + str(V) + str(Q)
		print '-'*5
		print str(T) + str(U) + str(R) + str(Q) + str(W)
		print 

```
