# Jupyter Lab Anaconda Env Not Available

#python #jupyterlab #troubleshooting

[Conda environments not showing up in Jupyter Notebook](https://stackoverflow.com/questions/39604271/conda-environments-not-showing-up-in-jupyter-notebook)

[@jorgejgleandro - Kernels from conda env not listed in JupyterLab kernel selection](https://github.com/jupyterlab/jupyterlab/issues/3951#issuecomment-454893558)

In the Anaconda Prompt, make sure you have ipykernel installed in your Anaconda base environment.  
Assuming "your_env" has the same name as the desired kernel, do:
```shell
$base conda activate <your_env>
$your_env python3 -m ipykernel install --user --name <your_env> --display-name <your_env>
```
