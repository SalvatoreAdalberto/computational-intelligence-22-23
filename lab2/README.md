# Lab2: Set covering using Genetic Algorithm
Salvatore Adalberto Esposito - Gabriele Iurlaro

### Representation
The defined problem is encoded as a list of tuples removing duplicates:

```python
all_states = list(set([tuple(x) for x in problem(5, seed=42)]))
```
Population is defined as a deque since it requires costant time for appending an individual.

For what concerns an individual: the usual bit-representation is straightforward for this problem:

- 1 means that the corresponding tuple(or list) has been picked in the solution
- 0 none.

The genome is encapsuleted in a `Individual` namedTuple, together with his fitness. The fitness is computed once for every individual at "creation time", to avoid inefficiencies.

### Fitness function

Fitness is defined as a tuple $$f = (covered, -weight)$$
Where covered is the number of items covered by the solution. I've tried different combination of this parameter:
  - a weighted sum of covered and weight plus a bonus if they reach the solution; this fitness function was slower than the presented one and results where worse, due to the difficulty in tunining the costants.
  - a tuple $$f = (covered, -weight, -mean_reps)$$ where mean_reps is the average of repetitions of each covered number in the genome; this fitness function proved to be quite ineffective since it converges to the same solution of the presented fitness function but requiring more time.

### Genetic algorithm

Several implementations have been tried: 

### Results

Then, we discuss a little bit the obtained result. For every problem, the number of generation required to reach the plateau is little(below 100).

| N    | w    | generation |
| ---- | ---- | ---------- |
| 5    | 5    | 23         |
| 10   | 10   | 55         |
| 20   | 29   | 34         |
| 100  | 216  | 41         |
| 500  | 1557 | 61         |
| 1000 | 3757 | 63         |