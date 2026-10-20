***ETC for Networked Time Delay Dynamical Systems of with Arbitrary Network Topology***
===
### Problem Formulation
Let $N \in \mathbb{N}_+$ be the number of nodes in this network. Consider the system or arbitrarily many coupled systems with a selection of those systems under event triggered control. 
$$
\begin{aligned}
&\dot x_i(t) = A_i x_i + \sum^N_{j=1}  \Gamma_{ij}  x_j (t- \tau(t)) + K_ix_i(t_{ik}), \quad i = 1,...,N
\end{aligned} 
$$
Where,
- $A_i \in \mathbb R^{n\times n}$ is a nonzero linear transformation modeling linear instantaneous dynamics.
- $\Gamma_{ij}\in \mathbb R^{n\times n}$ is a set of linear transformations modeling the linear delay dependance of system $i$ on $j$. Systems are always self coupled $\Gamma_{ii} \ne 0$, but dont need to be coupled with any other particular system so $\Gamma_{ij} = 0$ is permitted.
- $K_i \in \mathbb R^{n \times n}$ is the linear closed loop control transformation that maps the sampled state to a control response. A system need not be controlled, so $K_i =0$ is permitted.
- $t_{ik}$ denotes the event subsequence in time of the ETC of system $i$. 

Define $\sigma_i, \alpha_i, \beta_i > 0$ as engineered parmeters.

Define the ETC as follows for each control independantly:
$$
\begin{aligned}
&\text{ETC Sampling Error:} \quad \epsilon_i(t) := x_i(t_k) - x_i(t), \quad t \in [t_{ik}, t_{ik+1}), \quad \text{for } k\in \mathbb{N}  \\

& \text{Error Measure:} \quad \mathcal C_i (x_i(t), \epsilon_i(t)) := 2x_i^T P_iK_i\epsilon_i(t)- \sigma_i x_i^T P_i x_i \\

& \text{Event Threshold:} \quad \zeta_i := \alpha_i \exp({-\beta_i (t- t_0)}) \\

& \text{Event Subsequence:} \quad t_{ik+1} := \inf\{t_i \gt t_{ik} : \mathcal C_i(x_i(t),\epsilon_i(t)) \ge \zeta_i(t)\}
\end{aligned}
$$
Define the directed graph $\mathcal{G:= (V,E)}$ where:
$$
\mathcal V:=  \{i \in [1,N]\}, \quad \mathcal E:=\{(i,j) :  i,j \in [1,N], \Gamma_{ij} \ne 0\}
$$
Define for a node the reachable set of $i$ as $\mathcal R(i)$, and the directly connected set of nodes to $i$ as $\mathcal N (i)$. Define the following equivalence class:
$$
i \sim j \iff i \in \mathcal R(j) \cup \{j\} \text{ and } j \in \mathcal R(i) \cup \{i\}
$$
Call these equivalence classes $[i]$. Then define $\mathcal V^* := \mathcal V/\sim$.

Now define the edges:
$$
\mathcal E^* := \{([i],[j]) : (i,j) \in \mathcal E : [i] \ne [j]\}
$$
Define the the quotient graph:
$$
\mathcal G^* := (\mathcal V^*, \mathcal E^*)
$$
Define further the reachable set for a supernode on $\mathcal G^*$ as $\mathcal R{([i])}$ directly connected nodes for $i$ that themselves reach $i$, $\mathcal{D}(i)$, and the set of directly connected nodes of $i$ that do not themselves reach the node $i$, $\mathcal B(i)$. Formally:
$$
\mathcal D(i) := \{\ j \in \mathcal N(i) : i \in \mathcal{R}(j)\} \cup \{i\}, \quad \mathcal B(i) := \mathcal{N}(i) \setminus\mathcal{D}(i) 
$$

### Results
This section discusses the main results

#### Lemma 1: $\mathcal G^*$ is asyclic ***
proof excluded

Since $\mathcal G^*$ is a finite DAG, reachability is a partial order. With the graph being finite we extend this to any arbitrary topological total orderings from this partial ordering, call this arbitrary topological ordering $\pi$.


#### Lemma 2: Exponential Attractivity ***
Define: $||V_i||_t := \sup_{-\tau \le s \le 0}\{V_i(t+s)\}$ and let $V_i : [t_0-\tau, \infty) \to \mathbb{R}_{\ge0}$ be continuous functions such that:
$$
D^+V_i(t) \le -a_iV_i(t) + \sum_{j=1}^{n} c_{ij}||V_j||_t + \alpha_i \exp{-\beta_i(t-t_0)}, \quad i\in[1,n], \quad \forall t\ge t_0 \tag{C1}
$$
Assume that:
$$
a_i > \sum_{j \in \mathcal D(i)} c_{ij}, \quad i \in [1,n] \tag{C2}
$$
Fix in the topological order of supernodes $\bar M_i := \max\{\, M_i,\; \kappa_i,\; ||V_i||_{t_0} \, : i \in \mathcal V^*_i\}$, where leafs can be fixed direcetly and non leaves must be fixed by choosing $M_i, \kappa_i > 0$ sufficiently large such that:
$$
a_i > \sum_{j \in  \mathcal D(i)} c_{ij} + \frac{1}{\kappa_i}\sum_{j \in \mathcal B(i)} c_{ij}\,\bar M_j^* + \frac{\alpha_i}{M_i} \tag{E1}
$$
For each $i \in \mathcal V^*_i$ and then determining $\bar M_i$. The ordering ensures that $\bar M^*_j$ is always defined before this fixing occurs.
 
Let $\lambda_i$ which exists and is unique from $(C2)$, be the solution to:
$$
a_i = \lambda + \Big( \sum_{j \in  \mathcal D(i)} c_{ij} + \frac{1}{\kappa_i}\sum_{j \in \mathcal B(i)} c_{ij}\,\bar M_j^* \Big)\exp{\lambda\tau} + \frac{\alpha_i}{M_i} \tag{E2}
$$
Let:
$$
\Lambda_{[i]} := \{\lambda_i : i \in [i] \}   \cup
\{\beta_i : \alpha_i > 0, i \in [i]\},
\quad \Lambda_{[i]}^* := \min \Lambda_{[i]} \cup \bigcup_{j \in \mathcal R([i])} \Lambda_{[j]} , \quad

 \bar M_i^* := \max  \bar M_i \cup \bigcup_{j \in \mathcal R(i)} \bar M_j 
$$
Then:
$$
V_i(t) \le \bar M_i^*\, \exp(-\Lambda_{[i]}^*(t-t_0)), \quad \forall t \ge t_0 \tag{R1}
$$

Proof:
Proof excluded

#### Theorem ***
Define: $h_i > 0$ and $a_i := \sum_{j \in \mathcal D(i)} b_{ij} + h_i - \sigma_i$. 

Assume:
$$
h_i > \sigma_i \tag{As.1}
$$
Assume that for $P := Q^{-1}$, $Y := KQ$, and $W_i :=(A_i + K_i)^T P_i + P_i(A_i + K_i) + (a_i + \sigma_i)P_i$
$$
\begin{bmatrix} W_i & \Gamma_{i1}Q_1 & \Gamma_{i2}Q_2 & \cdots & \Gamma_{iN}Q_N \\ Q_1\Gamma_{i1}^T & -b_{i1}Q_1 & & & \\ Q_2\Gamma_{i2}^T & & -b_{i2}Q_2 & & \\ \vdots & & & \ddots & \\ Q_N\Gamma_{iN}^T & & & & -b_{iN}Q_N \end{bmatrix} \preceq 0 \tag {As.2}
$$
Then you get exponential attractivity of system $i$ to the zero energy state$^{(i)}$, and there is no zeno behaviour.$^{(ii)}$

##### Proof $(i)$ ***
Proof excluded

##### Proof $(ii)$ ***
Proof excluded
===
