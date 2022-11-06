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

The algorithm follows a 'strategy 2' approach in which the offspring is generated mutating or recombining parent population, added to the current population, and then only the best POPULATION_SIZE individuals are kept for the next generation.

Mutation rate and Selective Pressure (in this algorithm it refers as the number of individuals which joins a tournament in order to mutate or recombine: 'torunament_size') have been chosen to be 0.4 and 2. 
Other possibilities have been explored like:
  - having a dynamic MR as a function of the number of generations (under a certain number of gens it was low favouring recombination while after it was increased favouring mutations); proved to be poorely effective probably due to the dipendence from #genetrations, and not to a measure of the distance from good solution.
  - decresing a bit the selective pressure, inserting the possibility of having a tournament in which the 'winner' could be with a higher probability the fittest among selected, but also, with a lower probability, to select one individual randomly in order to increase exploration; I will keep trying tuning this implementation because even if it takes more time to converge, it could land to a better solution
  - defining a different crossover strategy, namely 'crossover2', in which recombination is performed not with a signle cut-point but filling each locus with the allele of a random parent; the representation of the problem makes this type of crossover very random so even if the child is effectively a recombination of the parents, it could end up not preserving any information of them; moreover this type of crossover requires almost 10x time than the classical one.
  - initially population was initialized randomly but it required a lot of generations in order to find a barely presentable solution. So 0 genome initialization was preferable under every point of view. 
  - a Steady state termination condition has been inserted, keeping track of the number of generations the fittest individual was unchanged, since most of the times solution was found in early generations.
  
### Results

The number of generation required to reach the plateau is little(below 100).

| N    | w    | generation |
| ---- | ---- | ---------- |
| 5    | 5    | 23         |
| 10   | 10   | 55         |
| 20   | 29   | 34         |
| 100  | 216  | 41         |
| 500  | 1557 | 61         |
| 1000 | 3757 | 63         |