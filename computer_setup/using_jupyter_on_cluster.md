Using Jupyter notebook on the cluster 

1) ssh onto cluster head node (e.g. login1)
```
ssh tswift@login1.molbiol.ox.ac.uk
```
2) Open tmux or screen session (this will keep your interactive job going if you loose connection)
```
# Check if already have tmux session open 
tmux ls 
# Open it if you do (change 0 to the number of the session you want)
tmux attach -t 0 
# Or create a new one (this puts you in a tmux window) 
tmux 
```
3) Get an interactive session on a node (might want to edit params on this ) e.g: 

```srun --cpus-per-task 2 --mem 64G --ntasks-per-node 1 --time 23:59:59 --pty bash```

4) When on node take a node of the node id (e.g. imm-wn6)
5) Load conda env and start juptyer lab or notebook e.g 

```
# activate conda environment 
conda activate test_python_env

# if using jupyter lab -> change port number 8545 to whatever you want e.g. 6767
jupyter-lab --no-browser --port 8545

# if using jupyter notebool -> change port number 8545 to whatever you want e.g. 6767
jupyter notebook --no-browser --port 8545
```
6) Copy the notebook address from the juptyer output e.g. http://localhost:8545/lab and paste into a browser on your local machine (it won't have any output at this point)

7) In a new terminal open an ssh tunnel from your local machine to the ccb server - make sure you update the port number 8545 to whatever you used in step 5 

```ssh -A -L 8545:localhost:8545 tswift@login1.molbiol.ox.ac.uk```

8) Then when on login1 through the tunnel in 7 open a subsequent tunnel to the node running jupyter -> again make sure you update the port number 8545 to whatever you choose in step 5 and the node id (e.g. imm-wn6) to whatever node jupyter is running on. 

```ssh -N -L 8545:localhost:8545 tswift@imm-wn6```
 
