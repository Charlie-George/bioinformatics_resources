Using Jupyter notebook on the cluster 

1) ssh onto cluster head node (e.g. login1)
```
ssh tswift@login1.molbiol.ox.ac.uk
```
2) Open tmux or screen session (this will keep your interactive job going if you lose connection) - link to brief tmux overview [here](https://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/)
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

4) When on node take a note of the node id (e.g. imm-wn6)
5) Load conda env and start juptyer lab or notebook e.g 

```
# activate conda environment 
conda activate test_python_env

# if using jupyter lab -> change port number 8545 to whatever you want e.g. 6767
jupyter-lab --no-browser --port 8545

# if using jupyter notebook -> change port number 8545 to whatever you want e.g. 6767
jupyter notebook --no-browser --port 8545
```
6) Copy the notebook address from the juptyer output e.g. http://localhost:8545/lab and paste into a browser on your local machine (it won't have any output at this point)
   

8) In a new terminal open an ssh tunnel from your local machine to the ccb server - make sure you update the port number 8545 to whatever you used in step 5 

```ssh -A -L 8545:localhost:8545 tswift@login1.molbiol.ox.ac.uk```

8) Then when on login1 through the tunnel in 7 run a subsequent ssh command to foward the output of the node running jupyter to your machine -> again make sure you update the port number 8545 to whatever you choose in step 5 and the node id (e.g. imm-wn6) to whatever node jupyter is running on. 

```ssh -N -L 8545:localhost:8545 tswift@imm-wn6```

9) Now refresh your browser where you pasted the jupyter link and it should work! Yay! If it doesn't make sure to check your ports and node names are correct
 
If you lose connection during the day - then tmux will ensure that your interactive session on the node and juptyer continue running on it, but you will need to reestablish the tunnel and port forwarding by rerunning steps 8 & 9. If you want to close your jupyter session on the command line you need to repeat steps 1 & 2 to attach the tmux session you created and stop the jupyter process. 

