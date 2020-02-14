---
layout: post
title:  "Solving ODEs Numerically With Python"
date:   2020-02-14 12:01:03 -0500
categories: Mathematics
---

Python's `scipy` library provides several computational methods of solving a variety of problems. Today, I learned how to solve first-order IVP problems using `scipy.integrate.solve_ivp`.

Consider a simple example: the position of a golf ball as it travels through the air.

```
def simple_golf(t, z):
    '''Input:
        z[0] = x(t)
        z[1] = y(t)
        z[2] = y'(t)
       Output is time derivative: 
       dx/dt = Vx (constant horizontal velocity)
       dy/dt = z[2] (i.e., y')
       dy'/dt = -9.81 (gravity)
    '''
    # Vx is defined globally
    return [Vx, z[2] , -9.81]
```

What we're defining here is a **dynamics function** that models our problem. That is, $$y'(t) = f(t, y(t))$$ in a ODE, and the dynamics function is the RHS.

Note: One confusing thing about this is that we're returning an array-like from the function. If you look at the `scipy` docs, they just say that the dynamics function most return an array-like, but don't specify why.

The answer is pretty much what you expect: We return an array-like because this is a vector-valued dynamics function that we're considering, as stated in the comments of the function. One could view this as three separate first order ODEs in the same system.