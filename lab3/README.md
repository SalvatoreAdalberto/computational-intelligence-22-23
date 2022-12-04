# LAB 3 - Nim
Salvatore Adalberto Esposito - Gabriele Iurlaro
## Task 3.1
The main idea of the hardcoded strategy is to divide the Nim-game in 2 phases:

Early game: in this phase, we try to remove the most from the row, but we will try to keep always a stick in it

Late game: in this phase, we will take all from the row, to finish the game early
The distinction is base on the completation, computed as the number of stick remaining on the boar divided by the total number of sticks.

## Task 3.2
We evolved two strategies:

`evolvable_strategy` is the one mentioned before, the parameter to evolve are:
`max_k`: a maximum amout of sticks
`turn_strategy`: when we turn strategies
`evolvable_random_strategy`: since the one before plays always the same, we introduced a bit of randomness in the play, resulting in slightly better result.


