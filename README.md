# BFTrainerSimu
A scheduler log replayer for BFTrainer evaluation

- This simulator replays real scheduler logs for evaluation of different DNN training scenarios and objective metrics. 
- The simulator uses exactly the same MILP implementation as it in the BFTrainer.
- Only the interaction between BFTrainer and main batch scheduler (i.e., main scheduler notifies BFTrainer when there are nodes become idle or preempted) is replaced with a log replayer. 

Target user of the simulator:

- Supercomputer provider: replay their logs to see if BFTrainer can successfully make use of the fragmented idle nodes. 
- BFTrainer users: Try their objective metric and DNN training scenarios (e.g., NAS, HPO) without requesting real resource access.
- Algorithm Developer/Contributor: Evaluate change and proposals without touching the physucal supercomputer and requiring support from the main scheduler.

# MILP solver
We provided two implementations of the MILP model:
- [PYTHON-MIP](https://www.python-mip.com) with open source (free) [CBC](https://github.com/coin-or/Cbc) solver.
- [gurobipy](https://www.gurobi.com/documentation/9.1/quickstart_mac/cs_grbpy_the_gurobi_python.html), the Gurobi Python Interface, with [Gurobi](https://www.gurobi.com) solver. Licensed required, one can use free trial or academia license for evaluation purpose.

Based on our preliminary benchmark, Gurobi is much faster than CBC when problem size is big (e.g., dozens of jobs on hundreds of nodes).
Otherwise, the time to solve is very similar between Gurobi and CBC when problem size is small.<br>

The PYTHON-MIP also supports using Gurobi as solver (license required as well) but slower than gurobipy in most cases especially when problem size is large.
Thus, one can use the free CBC when problem size is small, especailly for relatively small supercomputers. 
Otherwise, Gurobi with the gurobipy based implementation is recommended.
