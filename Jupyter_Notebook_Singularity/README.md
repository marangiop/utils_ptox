# JupyterLab inside Singularity (via 2-hop SSH tunnel)

1. Create conda environment with JupyterLab installed 
```shell
conda create -n jupyter_env python=3.8
conda activate jupyter_env
pip install jupyterlab
```

2. Get interactive node in lab queue
```shell
qlogin -q rg-el7
```

3. Start JupyterLab 
```shell
conda activate jupyter_env
jupyter-lab --no-browser --port=9000
#Do not close this terminal (terminal 1)!
```

8. Start 2-Hop SSH tunnelling on another terminal (if connecting from home Wi-Fi this will require turning on VPN connection)
```shell
ssh -L 9000:localhost:9000 <username>@ant-login.linux.crg.es -t ssh -L 9000:localhost:9000 <username>@<node-id>
```
9. Open an internet browser and go to `localhost:9000` to access JupyterLab.
If required, provide token displayed in terminal 1.

Always make sure to gracefully stop JupyterLab with `ctrl+C` and exit the lab node when done.

