## Setting up ssh 

- standard command = `ssh  <username>@<server.address.ox.ac.uk>`
- can add host name and address to `.ssh/config` file to save typing full address and options each time 
- can use public-private key pair to save entering password each time 

### ssh key pairs: 

- Key pairs consist of 2 parts 
1. A **private** file retained by you in your local home directory (e.g. `id_rsa`)
2. A **public** file which is uploaded to remote server you are connecting to (e.g. `id_rsa.pub`) 

- If it helps you can think of the private part being a key and the public part being a lock, the lock is not private, everyone can see it but only you have the key that allows you access.
- All ssh keys and config is stored in the hidden `.ssh` directory (`~/.ssh`)
- BASH has a command for generating keys 
```
cd ~/.ssh
ssh-keygen -t rsa -b 2048

# this will then say something linke enter a file in which to save the key
# its usually fine just to press enter and use the default file name unless you might have previously generated a key thats already named that and want to keep it.

# you will then be prompted for a passphrase
# please set one for maximum security we will add the password to your ssh-agent later so you don't have to type it all the time 
```

- note that different servers might require different ssh key encryption types - above the `-t` flag specifies `rsa`. This is now fairly old and newer more secure severs often now specify ecdsa  or something else (ed25519 for github for example)
- the `-b` specifies the number of bytes of the key, bigger is usually more secure  
- There is loads of info about ssh and key generation here https://www.ssh.com/academy/ssh-keys
- Once the keys are generated you upload the public key to the server 
```
ssh-copy-id -i ~/.ssh/id_rsa <username>@<server.address.ox.ac.uk>
# you will be prompted for your server password now (not the ssh password you just set)
```
- Next time you log on it will use your ssh password to gain access, but to avoid having to type this all the time too we can add the ssh password to an ssh authentication agent 
```
eval `ssh-agent -s`
ssh-add ~/.ssh/id_rsa
ssh -i ~/.ssh/id_rsa <username>@<server.address.ox.ac.uk>            
```
- Finally if you haven't already add the ssh connection details to your `~/.ssh/config` file 
```
# add something like this 
host <ccb1>
    hostname <server.address.ox.ac.uk>
    user <username>
    identityfile ~/.ssh/id_rsa 
```
- now you can log on using just `ssh ccb1` for example


## JADE: 
- Slurm 
- check queues: sinfo 
    - short (1 day time limit - 6 nodes)
    - long (7 Day time limit - 6 nodes)
    - jumbo 
    - gpu 
    - test

- get interactive node - e.g. for installing conda envs 
    - examples:
        - `srun --partition=short --cpus-per-task=4 --mem=32G --pty bash -i`
        - `srun --cpus-per-task 2 --mem 64G --ntasks-per-node 1 --time 23:59:59 --pty bash`
     
- need to change `.cgat.yml` to update default options for queues (time, cpus, default mem requested)

## CBRG
- tunnel jupyter notebook - use cbrglogin3 
    - ssh `<username>@<address.ox.ac.uk>`
    - open tmux and run notebook
```
tmux
conda activate <env_name>
juptyer notebook --no-browser --port <5353>
# copy the ip address
```
  - open tunnel 
  - `ssh -L <5353>:localhost:<5353> <username>@<address.ox.ac.uk>`
  - paste ip address into local chrome 


