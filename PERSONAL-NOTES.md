We have been collecting various ideas. Here's our docs on them:

# Bitmasking
DX300 can be used to bitmask numbers. For example:

- 100 on p0 -> 1
- 100 on p1 -> 10

# Additional registers
I think this is more theory at the moment but DX300 should be able to convert P registers into long term ones

# Event based wait
**Controller 1:**

```
mov 100 x0
```

**Controller 2:**

```
# Wait for signal
slx x0

# Flush signal
# DEV: As a bonus, we can use practical data on x0
mov x0 null
```

# 3 way jump

```
tcp acc 2
+ # Do branch 1
+ jmp SLEEP
- # Do branch 2
- jmp SLEEP
# Do branch 3

SLEEP:
slp 1
```
