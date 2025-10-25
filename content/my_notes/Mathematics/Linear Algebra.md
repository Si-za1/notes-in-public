---
title: Linear Algebra
draft: false
tags:
  - in-progress
  - math
reference: https://youtu.be/5oZ84mlt7tM
---
## Chapter 1: Vectors, Dot Product, and Geometry

The easier concept to understand the term vector. 


Imagine: 
If a movie streaming service wants to measure how similar three users' tastes are.

That's where vector comes to play. 
Vectors are the fundamental objects of linear algebra. They are not just arrows; they are how we represent data, from a point in space to a user's preferences.

**Our intuition** is that the angle `θ` between the vectors is a perfect measure of similarity. **A small angle means high similarity.** The dot product is the tool that lets us calculate this angle directly from the ratings.

So, the DOT product 

It has two definitions that we use together:

1. **The calculation formula.**
Multiply corresponding components and add them up. For vectors `a = [a₁, a₂, ..., aₙ]` and `b = [b₁, b₂, ..., bₙ]`: `a · b = a₁b₁ + a₂b₂ + ... + aₙbₙ`
2. **The Geometric Formula** , this is where you find your dot product i..e  the angle that we talked about earlier to understand whether something matches or not. 
`a · b = ||a|| ||b|| cos(θ)`

Where `||a||` is the magnitude (length) of vector `a`, calculated as `sqrt(a₁² + a₂² + ...)`.

We will use the first formula to get a number, then plug it into the second to find the angle `θ`.

Let's solve our movie similarity problem by finding the actual angles.

**Inputs:**

- `a = [5, 4, 1]`
- `b = [4, 5, 2]`

#### **Case 1: Comparing Similar Users (A and B)**

**Step 1: Calculate the dot product `a · b`.** `a · b = (5 * 4) + (4 * 5) + (1 * 2) = 20 + 20 + 2 = 42`

**Step 2: Calculate the magnitudes `||a||` and `||b||`.** `||a|| = sqrt(5² + 4² + 1²) = sqrt(25 + 16 + 1) = sqrt(42) ≈ 6.48` `||b|| = sqrt(4² + 5² + 2²) = sqrt(16 + 25 + 4) = sqrt(45) ≈ 6.71`

**Step 3: Solve for the angle `θ`.** We rearrange the geometric formula: `cos(θ) = (a · b) / (||a|| ||b||)` `cos(θ) = 42 / (sqrt(42) * sqrt(45)) = 42 / (6.48 * 6.71) ≈ 42 / 43.48 ≈ 0.966` `θ = arccos(0.966) ≈ 15.0°`

**Result:** The angle between User A's and B's preferences is about **15 degrees**. This is very small, confirming they have highly similar tastes.

So, now if we compare why some users have different taste . It means, their angle i.e. the angle between those user's preferences is high. 

**Using Numpy:**
![[Pasted image 20251025132148.png]] 
## Chapter 2: Linear Systems, Matrices, and Elimination

the origin of the "linear" in linear algebra and a core motivation for inventing matrices is to solve problems involving multiple linear relationships at once.

### The Motivating Problem

A coffee shop sells two custom blends.

- **Blend A** uses 300g of arabica and 100g of robusta beans per unit.
- **Blend B** uses 100g of arabica and 200g of robusta beans per unit.

Today, the shop has **11,000g** of arabica and **8,000g** of robusta in stock. How many units of each blend (`x` units of A, `y` units of B) can they make to use up all the stock?

### The Formalization: The `Ax = b` Form

First, we translate the word problem into a system of linear equations.

1. **Arabica equation:** `300x + 100y = 11000`
2. **Robusta equation:** `100x + 200y = 8000`

This system can be represented elegantly using matrix notation, `Ax = b`.

- **A**: The **coefficient matrix**. It contains the "recipes". `A = [[300, 100], [100, 200]]`
- **x**: The **vector of unknowns**. This is what we want to solve for. `x = [[x], [y]]`
- **b**: The **constant vector**. This is the available stock. `b = [[11000], [8000]]`

So, our system becomes: `[[300, 100], [100, 200]] * [[x], [y]] = [[11000], [8000]]`

If you perform the matrix-vector multiplication, you get the original two equations back. This `Ax=b` form is the standard way to represent linear systems.

### **The Algorithm: Gaussian Elimination**

Gaussian Elimination is a systematic procedure for solving `Ax=b`. The goal is to simplify the system into an "upper triangular" form (called **Row Echelon Form**), which is easy to solve.

We use a shorthand called the **augmented matrix**, `[A | b]`, and manipulate it using three allowed **Elementary Row Operations**:

1. Swap two rows.
2. Multiply a row by a non-zero scalar.
3. Add a multiple of one row to another row.

## Step-by-Step Example 

Let's solve the coffee problem.

**Step 1: Set up the augmented matrix.** `[ 300 100 | 11000 ]` `[ 100 200 | 8000 ]`

**Step 2: Simplify the rows (Rule 2).** The numbers are large. Let's divide Row 1 by 100 and Row 2 by 100 to make it easier. `R1 -> R1 / 100` `R2 -> R2 / 100`

`[ 3 1 | 110 ]` `[ 1 2 | 80 ]`

**Step 3: Get a 1 in the top-left ("pivot") position (Rule 1).** It's easiest to work with a leading `1`. Let's swap Row 1 and Row 2. `R1 <-> R2`

`[ 1 2 | 80 ]` `[ 3 1 | 110 ]`

**Step 4: Eliminate the entry below the pivot (Rule 3).** Our goal is to create a `0` where the `3` is. We do this by subtracting 3 times Row 1 from Row 2. `R2 -> R2 - 3*R1`

- `3 - 3*1 = 0`
- `1 - 3*2 = -5`
- `110 - 3*80 = 110 - 240 = -130`

The new matrix is: `[ 1 2 | 80 ]` `[ 0 -5 | -130 ]`

We have now reached Row Echelon Form. The system is "triangular."

**Step 5: Solve using back substitution.** Translate the simplified matrix back into equations.

1. From Row 2: `0x - 5y = -130` => `-5y = -130` => `y = 26`
2. From Row 1: `1x + 2y = 80`. We know `y = 26`, so we substitute it back in. `x + 2(26) = 80` `x + 52 = 80` `x = 28`

**Result:** The shop can make **28 units of Blend A** and **26 units of Blend B**.

**Using Numpy:**
![[Pasted image 20251025132235.png]] 