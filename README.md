# BFTrainerSimu
A simulator for BFTrainer evaluation

- This simulator replays real scheduler logs for evaluation of different DNN training scenarios and objective metrics. 
- The simulator uses exactly the same MILP implementation as it in the BFTrainer.
- Only the interaction between BFTrainer and main batch scheduler (i.e., main scheduler notifies BFTrainer when there are nodes become idle or preempted) is replaced with a log replayer. 

Target user of the simulator:

- Supercomputer provider: replay their logs to see if BFTrainer can successfully make use of the fragmented idle nodes. 
- BFTrainer users: Try their objective metric and DNN training scenarios (e.g., NAS, HPO) without requesting real resource access.
- Algorithm Developer/Contributor: Evaluate change and proposals without touching the physucal supercomputer and requiring support from the main scheduler.
