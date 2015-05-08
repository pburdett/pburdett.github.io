---
layout: post
title: An interesting Maths Problem
---

### The question

I recently came across an interesting maths problem, aimed at 12-13year olds. It read...

>Each different letter in the following addition sum represents a different digit from 0-9 inclusive (neither P nor T are equal to zero, and not the digits are used)

> P Q R D + T U V Q = T U R Q W

>Explaining your reasoning carefully, find which letters correspond to which digits.


### The mathematical solution

Let's start by re-writing the equation


         P Q R S  (a)
      +  T U V Q  (b)
      ----------------
       T U R Q W  (c)
 

Firstly, two numbers \\( \lt 10^{3} \\) cannot sum to \\( \gt 2 \times 10^{4} \Rightarrow T = 1 \\)

Since \\( T = 1, 1000 \lt (b) \lt 2000 \Rightarrow P = 8 \\) or \\( 9 \\) to ensure \\( (c) \gt 10^{4} \\)

I will introduce some carry notation. Assuming \\( k_{i} = 1 \\) or \\( 0 \\), the following equations hold:

\\[ S + Q = 10 \times k\_{1} + W \\]

\\[ R + V + k\_{1} = 10 \times k\_{2} + Q \\]

\\[ Q + U + k\_{2} = 10 \times k\_{3} + R \\]

\\[ P + T + k\_{3} = 10 \times k\_{4} + U \\]

Since \\( T = 1 \\), we know \\( k_{4} = 1 \\)

if \\( P = 8 \Rightarrow Q + U \\) must result in a carry \\( \Rightarrow k\_{3} = 1 \Rightarrow P + T + k\_{3} = 10 \Rightarrow U = 0 \\)

if \\( P = 9 \Rightarrow Q + U \\) might not result in a carry \\( \Rightarrow P + T + k\_{3} \gt = 9 + 1 + k\_{3} = 10 \\) or \\( 11 \\)

if \\( 11 \Rightarrow U = 1 \\) which is a contradiction as \\( T = 1 \\), but if \\( 10 \Rightarrow U = 0 \\)

Hence \\( U = 0 \\) 



Assume \\( k\_{3} = 1 \Rightarrow Q + k\_{2} = 10 + R  \Rightarrow k\_{2} = 1  \\) since digits are less than 10.
\\( \Rightarrow Q = 9 + R \\) which can only be solved if \\( R = 0 \\). Hence we have a contradiction.

Hence \\( k\_{3} = 0 \Rightarrow P + 1 + 0 = 10 \Rightarrow P = 9 \\)

\\( Q + k\_{2} = R \Rightarrow k\_{2} = 1 \\) since \\( Q \\) does not equal \\( R \\)

\\( Q + 1 + R + V + k\_{1} = 10 + Q + R \\)

\\( \Rightarrow V + k\_{1} = 9 //) Since  \\( P = 9 \Rightarrow V = 8 \\) and \\( k\_{1} = 1 \\)

\\( S + Q = 10 + W \\) and  \\( Q + 1 = R \\)

Now we shall go through some combinations...

Assume \\(Q = 2\\), then R = 3 => S = 8 + W => W = 0 or 1 Which is not possible as T = 1 and U = 0. Contradiction

Assume Q = 3, then R = 4 => S = 7 + W => W = 2 => S = 9. Which is not possible since P = 9. Contradiction

Assume Q = 4, then R = 5 => S = 6 + W => W = 2 or 3. If W = 2 => S = 8 or if W = 3 => S = 9. Both contradictions.

Assume Q = 5, then R = 6 => S = 5 + W => W = 2, 3 or 4. **If W = 2, then S = 7. This is a possible solution.** If W = 3, then S = 8 or if W = 4 then S = 9. Both contradictions.

Assume Q = 6, then R = 7 => S = 4 + W => W = 2,3,4 or 5. If W = 2 => S = 6; If W = 3 => S = 7; If W = 4 => S = 8l If W = 5 => S = 9. All contradictions.

Assume Q = 7, then R = 8. Contradiction.

Hence the solution is **Q = 5, R = 6, W = 2, S = 7**.

The solution is therefore...

	  9567
	+ 1085
	------
	 10652




### The python implementation

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
