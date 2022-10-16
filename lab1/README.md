Lab 1 - Set Covering

Salvatore Adalberto Esposito - Gabriele Iurlaro

We used a best first algorithm and the used heuristic assigns a higher cost to those states in which the amount of missing (not yet covered) numbers is larger.

Starting idea was to use A* algorithm with the same heuristic, which provided better results in terms of visited nodes and minimization of the weights, but it didn't find a solution in a reasonable amount of time with N=100, 500, 1000.
