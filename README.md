In developing the evolutionary algorithm needed to determine the closest approximate solution to the optimal one for the TSP problem, I was inspired by the research paper written by professors Tao and Michalewicz. 
They introduced a new type of crossover operator called "inver-over," which I chose to be the core of my algorithm.

In each generation, for each individual in the population, a city c is randomly selected.

Selection and inversion loop: If the if branch is entered (with probability p), the second city c'
is selected from the remaining cities in the first individual. 
If the else branch is entered (with a probability complementary to p), another random individual is chosen 
and the second city c' is chosen as the city following c in this second individual.

Adjacency check: Before performing the inversion, it is checked whether c and c'
are already adjacent in the first individual. 
If they are adjacent, the loop is exited. 
If they are not adjacent, the subsequence between c and c'
is inverted in the first individual. 
After the inversion, c is updated with c', and the loop repeats, selecting a new 
c' starting from the just updated c.

Fitness Improvement Check: At the end of the loop, if there is an improvement in fitness, the individual in the population is replaced with its improved version.

In practice, the inver-over crossover is representative of the approach used in modern evolutionary algorithms because it doesn’t strictly apply a single genetic operator (mutation or crossover), instead, it combines them by controlling their application with a certain probability p. 
It uses inversion mutation (which isn’t too drastic, as it only reverses the order of a subsequence, thus keeping most cities in their original proximity in the sequence, which is crucial in TSP). 
This approach applies mutation to change the starting configuration while preserving enough connections between cities in a sequence that’s good in terms of fitness because these connections are important.
The crossover attempts to maintain the adjacency of cities in the inverted subsequence of the first individual, as well as the adjacency of cities c and c' in the second individual. 
The fact that the inversion boundaries in the first individual are chosen based on the adjacency of c and c' in the second individual ensures that the choice isn’t entirely random but rather strategically aimed at being heuristically effective, since it tries to preserve the adjacency of c and c' from the second individual.

The inver-over crossover is designed to apply two types of variation—inversion mutation and crossover—without strictly adhering to just one.  
By using a selection probability p, it dynamically chooses which method to apply, balancing exploration (through mutation) and exploitation (through crossover). This combination allows for small adjustments in solutions preserving connections between cities that contribute to a high fitness score.
The inversion mutation flips the order of a subsequence, introducing variation without a complete overhaul. 
This is crucial in the TSP since it allows configuration changes while preserving geographical proximity between nearby cities.  
Maintaining many of the original connections helps avoid destroying beneficial structures, which is critical for optimization problems where good solutions are often similar to one another.

When crossover is applied by selecting inversion boundaries based on the position of c and c' in the second individual, inver-over avoids randomness by using heuristic information from another individual.  
This ensures that the inverted subsequence retains neighborhood relationships that already exist in the second individual enhancing the chances of improvement through structured rather than entirely random configurations.

The idea of leveraging the relative positions of c and c' in the second individual is based on the heuristic that these adjacent cities likely form a beneficial connection for fitness.  
By avoiding drastic changes, the operator can preserve advantageous structures progressively optimizing the starting solution without breaking configurations that might already be close to optimal.

In addition to all this, to ensure that the initial population of 10 individuals from which the evolutionary algorithm starts is not entirely random, I chose to generate 9 individuals randomly through simple permutations and 1 individual as the solution of the greedy algorithm, whose execution is very fast and therefore does not introduce any noticeable delay before the start of the evolutionary algorithm's execution.

In summary, the inver-over crossover exemplifies a modern evolutionary approach: it doesn’t strictly follow one genetic operator but modulates crossover and mutation adaptively introducing targeted changes and preserving beneficial connections. 
This ability to balance exploration with exploitation of information in the population makes inver-over particularly effective for TSP.


The results that I got are the following ones:
| Country File  | Distance (km)         |
|---------------|-----------------------|
| vanuatu.csv   | 1345.544956473311 km  |
| italy.csv     | 4207.504730128662 km  |
| russia.csv    | 33907.84385417768 km  |
| us.csv        | 41025.28007127058 km  |
| china.csv     | 56414.62442982023 km  |

