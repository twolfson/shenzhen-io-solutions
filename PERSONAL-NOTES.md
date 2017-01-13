We have been collecting various ideas. Here's our docs on them:

# Bridges
As insighted by forums, all crossings are horizontal and vertical

For any bridge that you want horizontal, we can use a vertical one instead:

```
  |        |
----- =  --|--
  |        |
```

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

# Inline labels
As discovered via forums, labels can be inlined (main concern is line length). For example:

```
SLEEP:add 1 # Label = "SLEEP"
slp 1
```

# 3 way jump
Being direct and label-less is more efficient at lines:

```
tcp acc 2
+ # Do branch 1
- # Do branch 2
teq acc 2
+ # Do branch 3

slp 1
```

as opposed to:

```
tcp acc 2
+ # Do branch 1
+ jmp SLEEP # EXTRA
- # Do branch 2
- jmp SLEEP # EXTRA
# No `teq acc 2` here but it's 2 to 1 (3 incl label)
# Do branch 3

SLEEP: # EXTRA
slp 1
```

# Wiring under components
Sometimes we ge stuck in layout constrained spaces. After glancing at the subreddit, we found how to save a good chunk of space. To view the wires under components, use `<Tab>`

**Normal long wiring setup:**

```
    +------+
/---|      |
| /-|      |
| | +------+
| | +------+
| \-|      |
\---|      |
    +------+
```

**Under components wiring:**

```
    +------+
   -|-\    |
  /-| |    |
  | +-|----+
  | +-|----+
  \-| |    |
   ---/    |
    +------+
```

# X inputs can be slept through
We can read an entry in an X packet, sleep, and then read the next one still. It's weird but it works:

Attribution to subreddit

```
|[2]| 1 | 4 |
mov x0 null
|[2]|[1]| 4 |
slp 1
|[2]|[1]|[4]|
mov x0 null

```
