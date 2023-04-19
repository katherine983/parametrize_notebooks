# parametrize_notebooks
 Tutorial discussing how to parametrize a jupyter notebook with papermill including tips and tricks for getting the most out of it. Subtopics include:
 - using cell tags
 - using a conda environment with a jupyter notebook
 - parameterize notebook
 - use a yaml file to feed parameters
 - outputing notebook file as html using nbconvert
 - pipe papermill execution to nbconvert
 
 ## Requirements
 - python >= 3.7
 - papermill 
 - jupyter notebook
 - ipykernel
 
 ## Install papermill
 With conda
 ```console
 foo@bar:~$ conda install -c conda-forge papermill
 ```
 With pip
 ```console
 foo@bar:~$ python3 -m pip install papermill
 ```
 
 ## Using Cell Tags in a Jupyter Notebook
 
 A list of useful cell tags for controling the look of HTML output. 
 
Tags with 'hide' will hide the content with a toggle button 

 - hide-input tag to hide the cell inputs

 - hide-output to hide the cell outputs

 - hide-cell to hide the entire cell
 
 Whereas tags with 'remove' remove the content from view altogether
 
 - remove-cell to remove cell and its output from the view
 
 - remove-input to remove the cell contents from view but keep the output

 
 
 ## Setting the Notebook Environment to Run in a Conda Environment
 
 To get a jupyter notebook to run within a specific conda environment instead of the base environment you need to set the ipykernel.
 
 From within the conda environment, install the package ipykernel if not already installed.
 ```console
 foo@bar:~$ conda activate myenv
 (myenv) foo@bar:~$ conda install -c conda-forge ipykernel
 ```
 Then run the following command to make the conda active conda environment available as a kernel for jupyter notebook to run.

 ```console
 (myenv) foo@bar:~$ python -m ipykernel install --user --name=myenv
 ```
 Now this environment will be available within the jupyter notebook. To set this environment as the notebook kernel either launch jupyter   notebook from within the environment,
 ```console
 (myenv) foo@bar:~$ jupyter notebook
 ```
 or set it when creating a new notebook,
 
 ![New Kernel](jupyter_new_kernel.png)
 
 or set it from within an active notebook.

 ![Within_Kernel](jupyter_within_kernel.png)
 
 ## Use papermill from command line
 
 Run papermill from the CLI to execute a notebook with parameter values and output as a new file using this basic syntax.
 
 ```console
 foo@bar:~$ papermill template.ipynb output.ipynb -p param1 1.0 -p param2 True
 ```
 
 For our example using the chaos_game_template.ipynb file, we will use the below command:
 
 ```console
 foo@bar:~$ papermill chaos_game_template.ipynb chaos_game_defaultRNG.ipynb -p LCG 
 ```
 
 If you can't remember what parameters are available to set in the notebook you can run the below command to get a description. Papermill will infer the parameters based on the parameters cell.
```console
foo@bar:~$ papermill --help-notebook chaos_game_template.ipynb
Usage: papermill [OPTIONS] NOTEBOOK_PATH [OUTPUT_PATH]

Parameters inferred for notebook 'chaos_game_template.ipynb':
  RNG: Unknown type (default 'default_rng')
  SEED: Unknown type (default 2653589793)
  VERTICES: Unknown type (default 4)
  COORDS: Unknown type (default 3000)
```