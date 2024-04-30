# Molecule-Generation-using-Graph-NN
Generating molecules using Graph Neural Networks trained on the QM9- Quantum Mechanics dataset.

Trained three types of molecule properties:
1. Molecule Linker
2. Bond classifier
3. Node and edge generator

Pls git clone the other files from this repository:
https://github.com/PietroMSB/MG2N2/tree/master

# Requirements
To run the code, you will need a python>2.6 (Note: python 3.7 worked for us) distribution with the following python packages:
Tensorflow
Numpy
Scipy
Matplotlib
Networkx
We used the following package versions:
numpy==1.19.2
scipy==1.5.2
matplotlib==3.3.2
networkx==2.5
tensorflow==1.14.0

# data setup
QM9 data is provided in a "raw" format, to save space and downloading time. The script "translate_dataset.py" will process the dataset into the right format. The code can be easily adapted to be used on other datasets by substituting the dictionaries that map atom symbols and chemical bond categories to numerical labels, and adapting the input/output dimensions of the neural networks, in accordance to the atom symbols and bond categories found in the dataset under analysis.

# utility scripts
The "graph_decomposition.py" and "molecule_drawer.py" python files contain utilities for the other scripts. In particular, "molecular_drawer.py" provides some routines for sketching molecular graphs with networkx, mainly for debugging purposes. For high-quality images, we suggest drawing the molecules directly with Rdkit. "graph_decomposition.py" provides a set of functions to renumber the nodes with the algorithm described in the the paper, to extract the generation sequence of graphs from each molecular graph, and other related utilities. Please note that these scripts also require a little adaptation when switching from one dataset to another (for instance, the atom symbol -> one-hot vector mapping should be manually specified).

# network training
The script "train_generator.py" trains the generator module. The script "train_bond_classifier.py" trains the edge classifier module. The script "train_linker.py" trains the extra edge generator module. The hyparparameters of each module are declared in the first part of the corresponding script. The trained modules are saved into a "Temp/Modules" folder.

# graph preprocessing
The graph preprocessing operations are computationally demanding and take some time to complete. Thus, two operational modes ("short" / "full") are provided for each training script. When running in "full" mode, all the preprocessing operations will be executed, and the preprocessed data will be saved in the "Temp/Batches" folder, in the form of ready-to-load batches of training/validation/test graphs. When running in "short" mode, the script will skip the preprocessing operations and load previously compiled batch files. This means that preprocessing operations need to be carried out only during the first run of each script, or when a parameter which has an effect on preprocessing is changed. Each GNN module has its own subfolder for saving batch files.

# graph generation
The script "generate_graphs.py" generates a batch of graphs, exploiting the three modules which had been previously saved in the "Temp/Modules" folder. The hyperparameters of the modules are declared at the beginning of the script. At least one trained instance of each module is required to run this script.

# References:

https://doi.org/10.1016/j.neucom.2021.04.039
