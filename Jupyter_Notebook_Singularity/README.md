# Jupyter Notebook inside Singularity (via 2-hop SSH tunnel)

1. Install Vagrant on your laptop

2. Start Vagrant VM and connect to it

```shell
vagrant up
vagrant ssh
```

3. Create Singularity image
```shell
singularity shell jupyter.sif image.def
```

4. Copy Singularity image from Vagrant VM into host

5. Copy Singularity from host to `ant-login` cluster

6. Get interactive node in lab queue and load Singularity module
```shell
qlogin -q rg-el7
module load Singularity/3.8.3
```

7. Start Singularity shell and start Jupyter notebook
```shell
singularity shell jupyter.sif
jupyter notebook --no-browser --port=9000
#Do not close this shell!
```

8. Start 2-Hop SSH Tunnelling on another terminal
```shell
ssh -L 9000:localhost:9000 <username>@ant-login.linux.crg.es -t ssh -L 9000:localhost:9000 <username>@<node-id>
```

10. Open an internet browser and go to `localhost:9000` to access jupyter Notebook
If required, provide token for jupyter notebook displayed in Singularity shell 

Always make sure to gracefully stop jupyter notebook with `ctrl+C` and exit the lab node when done.

