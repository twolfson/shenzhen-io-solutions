Emails contain new info for code. Here's some snippets:

# gen
Pulse a simple pin for X seconds on, then Y seconds off

```
gen P R/I R/I
```

**Example:**

```
gen p0 3 2
# Runs:
# mov 100 p0
# slp 3
# mov 0 p0
# slp 2
```

# `@` conditional
One-time conditional:

```
@instruction goes here
```
