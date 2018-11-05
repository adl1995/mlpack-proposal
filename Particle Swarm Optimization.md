

**Particle Swarm Optimization**
=========================

* Organization: mlpack

Student information
-------------------

### Personal details ###
* **Name**: Adeel Ahmad
* **Email**: adeelahmadadl1995@gmail.com
* **Homepage**: [https://adl1995.github.io](https://adl1995.github.io/)
* **GitHub handle**: adl1995
* **IRC (#mlpack(?))**: adl1995
* **Interests and hobbies**: Running, Cycling, Reading, Cooking, Automating repetitive tasks 
* **Timezone**: UTC +05:00

### Academic details ###
* **University**: National University of Computer and Emerging Sciences, Islamabad
* **Enrollment date**: August 01, 2014
* **Graduation date (expected)**: August 01, 2018

### Experience and Background
##### Programming language proficiency

| Language       | Proficiency | Experience (years) |
|:--------------:|:-----------:|:------------------:|
| Python         | 4           | 3                  |
| C++            | 3           | 2                  |
| PHP            | 4           | 3                  |
| Assembly (x86) | 2           | < 1                |
| JavaScript     | 3           | 2                  |
| LaTeX          | 1           | 1                  |

##### Google Summer of Code 2017
I was a participant in Google Summer of Code 2017 [1] with the OpenAstronomy organization. My project involved the design and development of a Python client for Hierarchical Progressive Surveys (HiPS) [2], which is a scheme for describing astronomical images, source catalogues, and three-dimensional data cubes to manage large volumes of heterogeneous data. The package [3] enabled users to view astronomical figures in an interactive environment. I also maintained an extensive blog [4] throughout this period.

During the tenure of three months, I acquired a great deal of knowledge about software design principles and testing software from a user perspective. One major part of the development process was to write automated test cases and contiguously integrating code using Travis CI. Furthermore, I also composed API and user-level documentation using Sphinx [4].

##### Full-Stack Web Developer
Moreover, I have been a Full-Stack web developer for almost three years and have worked on multitude of projects ranging for SaaS to e-commerce websites. I work remotely on Upwork [5] and Fiverr [6]. My clients are either IT organizations or independent contractors. Besides web development, I also work on web automation and data scraping using `Selenium` and `BeautifulSoup`.

The skills that I acquire are through self learning and consistency. My GitHub profile [7] contains some of my other open source work.

##### Open Source contributions
Apart from the hips repository [3], where I have been contributor till GSoC 2017, I have made small contributions to these projects: OpenCV [8], libLAS [9], Jailhouse [10], Jupyter notebook [11], and axios [12].

##### Relevant coursework
My interest in machine learning sparked from taking my college courses: Data Mining and Deep Learning, which contained similar content as Stanford's CS229 and CS231n, respectively. The course content included but was not limited to: gradient descent (vanilla, mini-batch), linear, softmax, and SVM classifiers, Bernoulli distribution, convolutional neural networks, and recurrent neural networks (RNNs, LSTM). I also made a blog post explaining the various activation functions used in neural networks [13].

Apart from this, I am also enthusiastic about Computer Vision. My final year project involves implementing a structure from motion pipeline using a monocular camera [14]. To learn all the intricate steps involved in this process, I followed Robotics: Perception course on Coursera [15]. Image processing algorithms have always fascinated me, to quench this fascination I implemented numerous filters (Gaussian, Sobel, Prewitt, Laplacian), edge detectors (Canny, Marr Hildreth), morphological operators (Convex hulling, Erosion, Dilation), and object detectors (Generalized Hough transform, simple convolution) [16, 17]. These were implemented from scratch making use of  the ``NumPy`` Python library. The most interesting algorithm I implemented was Generalized Hough Transform [18]. I was amazed to see how something simple as the equation of line could lead to detection of objects in images.

My résumé [19] contains a more detailed overview on my interests and courses.

> What are your long-term plans, if you have figured those out yet? Where do you hope to see yourself in 10 years?

There is a major technical revolution coming in the near future, --but no one can say for sure if this will happen in the next 10 years--. I believe this breakthrough will come from the domain of artificial intelligence. 

However, instead of just speculating the future, I want to play a part in shaping it. I see myself as someone who has a good grasp in machine learning domain, and is constantly applying his skills to contribute towards its development.

> Describe the most interesting application of machine learning you can think of, and then describe how you might implement it.



### Project Proposal

Particle swarm optimization	is an optimization technique inspired by the social flocking of birds. The problem consists of a population of particles, where each is assigned a unique position and velocity. To achieve convergence, the algorithm tries to update the particle's position and velocity in a way that allows it to reach the global or local best solution. 

#### Objective

There exist several variants to particle swarm optimization. In the algorithm proposed by Eberhart and Kennedy [20], the group of particles are represented as a swarm, where all particles are attracted towards the global optima. Each particle keeps track of its best position, and moves through the solution space, evaluating its position along each step. Secondly, the particle keeps track of the global best position that was found by one member of the swarm, and this information is available to all swarm particles

A solution is already proposed for the global best PSO variant for unconstrained problems [21]. So, one objective of this project is to extend this implementation to handle constrained problems, for which an API is proposed below. Another objective is to implement other variants of PSO. I propose to implement the local best PSO and PSO with Velocity Adaption, proposed by S. Helwig et al. [22].

The implementation has to be backed up with extensive test cases including a diverse set of problems from convex optimization machine learning algorithms e.g. logistic regression and neural networks to low dimensional optimization functions.

If the implementation is completed before the proposed timeline, support for initialization techniques will be added, as the convergence of PSO greatly depends on the parameter's tuning. In regards to this, several solutions have been proposed in [], which try to find the best set of hyperparameters using evolutionary algorithms.

#### Problem description

Particle swarm optimization is similar to genetic algorithms, except it does not provide genetic operators like crossover and mutation. Instead, it updates particles with the internal velocity (see equation x). In the implementation proposed by Eberhart and Kennedy [20], both the particle position and velocity are initialized with uniform random numbers. Initially, the algorithm updated particle velocity on the basis of its nearest-neighbor, however, it was found that this technique made the particles to settle on a unanimous, unchanging direction. To account for this undesired behavior, a stochastic variable called "crazniesss" was introduced. --These include the social and cogninitive acceleration which produce a variation in velocity at each iteration.-- The current implementation treats the group of particles as a swarm, which can be visually compared with a flock of birds. Each particle keeps track of its best position over the entire run, called its `pbest` value. This conceptually resembles autobiographical memory, as each individual remembers its own experience. Similarly, velocity adjustment associated with `pbest` has been called "simple nostalgia" in that an individual tends to return to the place that most satisfied it in the past. The global best position or `gbest` is conceptually similar to publicized knowledge, or a group norm, which individuals seek to attain.

The cognitive (`pbest`) and social (`gbest`) elements have an associated acceleration, which are set following a heuristic. These stochastic variables produce a variation in velocity at each iteration.
...

#### Handling constrained problems

Similar to other nature-inspired techniques like evolutionary computation, PSO in its original form is designed to handle unconstrained problems [23] i.e. they lack the ability to include feasibility information of solutions in their fitness values. The common approach to deal with constraints is by using a penalty function, which aims to decrease the fitness of infeasible solutions. Another approach is to create a separate distinction between objective functions and constraints, one of this approach was proposed by Toscano and Coello [24] for the global best PSO where the leader is chosen based on the lowest number of violated constraints.

It is known that for constrained problems the probability of leaving the bounded-search space largely depends on velocity. Thus, if we are somehow able to control / decrease it, we can enforce the particles to remain within the boundaries enforced by the search space. However, this can lead to slow progress of the algorithm. The velocity adaption proposed in [25] shows that a large progress can be achieved with higher velocities. The low velocity is only attained if the algorithm observes to have difficulties for finding better solutions. Adaption of velocity is similar to the step size in evolution strategies. A success factor is introduced which accounts for the amount of progress made during the last iterations. It is considered a success when the particle's private guide(?) is set to its current position. If the new particle position and the private guide are of equal fitness, the private guide is then updated with a probability of $1/2$. If an improvement is found in the last iterations, the velocity is increased, otherwise, it is decreased.

The success rate of the algorithm for $n$ iterations is given by $SuccessCounter/(n * m)$, where $m$ is the number of particles. If the observed success rate is higher than a given threshold (called `SuccessProbability`) the velocities are increased by a factor of $2$, otherwise, the velocities are scaled down by a factor of $1/2$.

##### Implementation

There a two main design choices in the implementation of constrained problems (bounded?). One solution is to make use of lambda functions. This provides user the flexibility to define constraints and pass it to the optimizer. The lambda functions can be defined as below:
```cpp
auto constraint = [](double x) { return x < 3; };
```
The user can either define multiple constraints by providing multiple lambda functions, which the optimizer can handle using variadic templates [26], by making use of type expansion. An example is shown below:

```cpp
template<typename T>
bool constraintCheck(T v) {
  return v(3);
}

template<typename T, typename... Args>
bool constraintCheck(T constraint, Args... args) {
  return constraint(3) && constraintCheck(args...);
}

int main() {
  auto constraint1=[](int x){ return x < 3; };
  auto constraint2=[](int x){ return x > 3; };

  constraintCheck(constraint1, constraint2);
}
```
Another option for the user is to provide multiple constraints in a single lambda function, such as:
```cpp
auto constraint = [](double x, double y) { return x < 3 && y > 2; };
```
However, this might restrict the user in that they won't be able to modify constraints once the algorithm has begun execution(?). --This same could also be achieved by using Substitution Failure Is Not An Error (SFINAE) technique, but this has the restriction ...---

### API Design

mlpack employs a policy-based design numerous optimizers e.g. CMAES [27], Frank-Wolfe [28]. This meta-programming technique allows the algorithm to chose the variant on basis of the template parameter. Additionally, each variant requires a different initialization technique. For example, the constriction factor variant of PSO requires the cognitive and social acceleration for computing $k$ i.e. the constriction factor. Whereas, variants such as inertia weight do not require such initialization(explain more?). The currently proposed solution [21] is to provide dummy parameters to a class method when they are not required.

### Timeline

1 week - preliminary reading
1 week - Implmenet the lbest PSO for unconstrained problems with test cases
2 weeks - Implement the PSO with Velocity Adaption with extensive documentation and test cases
1 week - Create API which can handle constrained problems for the implemented PSO variants
1 week - Create problems of varying dimensionality with constraint bounds and test the constraint based API

1 weeks - Implement an initialization technique that produces good results for a variety of problems
2 weeks - Understand and implement the --- variant of PSO
1 week - Optimize the implementation especially steps involving velocity and position udpates
0.5 week - Create diverse examples to allow users get quickly started
1 weeks - Benchmark the performance on the basis of factors like accuracy, execution time, initialization techniques, etc.

### References
[1] HiPS client for Python https://summerofcode.withgoogle.com/archive/2017/projects/5440053895495680
[2] Hierarchical progressive surveys https://www.aanda.org/articles/aa/pdf/2015/06/aa26075-15.pdf
[3] Python astronomy package for HiPS https://github.com/hipspy/hips
[4] Sphinx documentation contents http://www.sphinx-doc.org/en/master/contents.html
[5] https://www.upwork.com/freelancers/~018e56b8591046f889
[6] https://www.fiverr.com/adl1995
[7] https://github.com/adl1995
[8] https://github.com/opencv/opencv/commits/master?author=adl1995
[9] https://github.com/libLAS/libLAS/commits/master?author=adl1995
[10] https://github.com/siemens/jailhouse/commits/next?author=adl1995
[11] https://github.com/jupyter/notebook/commits/master?author=adl1995
[12] https://github.com/axios/axios/issues/853
[13] An overview of activation functions used in neural networks https://adl1995.github.io/an-overview-of-activation-functions-used-in-neural-networks.html
[14] Structure from Motion pipeline https://github.com/reconstruct3d/SfM
[15] Robotics: Perception | Coursera https://www.coursera.org/learn/robotics-perception
[16] An implementation of Marr Hildreth and Canny edge detector https://github.com/adl1995/edge-detectors
[17] Multiple Choice Questions detecor https://github.com/adl1995/exam-mcq-recognitions
[18] An implementation of Generalised Hough transform https://github.com/adl1995/generalised-hough-transform
[19] Résumé https://adl1995.github.io/personal/resume.pdf
[20] Particle swarm optimization, by Kennedy et al. http://ieeexplore.ieee.org/document/488968/?reload=true
[21] Introduce Particle Swarm Optimization for unconstrained problems https://github.com/mlpack/mlpack/pull/1225
[22] Particle Swarm Optimization with Velocity Adaptation, by S. Helwig et al. http://ieeexplore.ieee.org/document/5329547/
[23] Looking Inside Particle Swarm Optimization in Constrained Search Spaces, by Jorge et al. https://pdfs.semanticscholar.org/5962/a6dba4776870f6bf2ad79b77e67f4dc1f628.pdf
[24] A Constraint-Handling Mechanism for Particle Swarm Optimization, by Gregorio et al. https://pdfs.semanticscholar.org/be9a/76f0d07c4dc137a7e2f1b9d0f857b56eac89.pdf 
[25] Velocity Adaptation in Particle Swarm Optimization by Helwig et al. http://ieeexplore.ieee.org/document/5329547/
[26] Variadic template https://en.wikipedia.org/wiki/Variadic_template
[27] CMAES https://github.com/mlpack/mlpack/tree/master/src/mlpack/core/optimizers/cmaes
[28] Frank-Wolfe https://github.com/mlpack/mlpack/tree/master/src/mlpack/core/optimizers/fw


