# suppmaterial-practitioners-perceptions-of-energy-consumption-on-stack-overflow
Supplemental materials for paper "How do Practitioners Perceive Energy Consumption on Stack Overflow?".

# Introduction
We organize the replication package into three file folders:
1. Experiment: this folder contains code for our main experiment (i.e., collecting extensions, selecting representative extensions, and measuring the extensions);

2. Analysis: this folder contains code for two parts:

	2.1 Browser Performance Evaluation: the statistical methods (i.e., the wilcoxon signed-rank test and the Cliff's Delta test) and the change ratio calculation;
	
	2.2 Linear Mixed Effects Model: factor selection helper, model optimization, and model builder.
	
3. Results: this folder contains the extension information stored in database, the clustering result in an excel file, extension selection steps in an excel file, installation packages of extensions, raw measurement data, and saved linear mixed effects models for our paper;

Our code is based on the following packages and versions:
* Python: 
* Numpy: 
* Pandas: 
* Sqlite3: 
* Scipy: 
* Simpledorff: 
* NLTK:
* Gensim:
* Tqdm:
* Spacy:
* PyLDAvis:
* Matplotlib:
* Seaborn:
* Operator:
* Sklearn:
* Functools:
* Re:


# Experiment
This part contains code for our main experiment in collecting the extension information from the Chrome Web Store, selecting representative extensions, and measuring the performance changes of the representative extensions. All code could be found under the experiment folder.

1. Crawler script

	This script (``collect.py``) is an automated script used to collect information of all extensions in the Chrome Web Store.

2. Extension Selection

	This script (``selecting representative extensions.ipynb``) guides the process of selecting extensions step by step.

3. Measurement

	This script (``measure.py``) is used to monitor the changes of the browser performance in terms of the page load time, the page load energy consumption, and the stabilized energy consumption.

# Analysis
This part contains code and materials for processing the dataset. The materials are introduced in two parts: Performance Evaluation (for RQs 1 and 2) and Linear Mixed Effects Models (for RQ3). All code could be found under the preprocessing folder.

  ## Performance Evaluation
  This part contains code for processing the measured raw data (for RQ1 and RQ2). The script ``performance evaluation.ipynb`` guides to process the raw data step by step and exports the processed result as an excel that will be used for the Linear Mixed-Effects Model in RQ3. Specifically, this script consists of three parts:
  
    1. Normalization

    2. Statistical analysis
      
    3. Performance change ratio
    
  ## Linear Mixed-Effects Models
  This part contains the code for constructing the linear mixed-effects model in RQ3. 
  
  Use ``correlation and redundancy.R`` to perform correlation and redundancy analysis for the fixed effects. 
  
  ``helper.ipynb`` is used to determine the best converge random effects (e.g., (1|random) and (random1|random2) ). 
  
  Following the steps, input the result from ``helper.ipynb`` to ``buildHelp.R`` or ``buildHelp2.R`` to automatically filter the converged variables. 
  
  Lastly, using ``builder.R`` to conduct a stepwise elimination to obtain the optimal formula.
The defined optimal formula is required to use ``lmer4`` to construct model again and use ``Anova`` and ``fixef`` provied in ``car`` to find the results and effect. ``Summary(model)`` may be useful as well.

# Results
This part contains the output data from our main experiments. All output files could be found under the results folder.
This folder contains the extension information stored in database, the clustering result in an excel file, extension selection steps in an excel file, installation packages of extensions, raw measurement data, and saved linear mixed effects models for our paper;

1. Extension information

	The collected information of all extensions in the Chrome Web Store are presented in the forms of SQL and database, which can be found in ``extensions.sql`` and ``plugin.db``.

2. The result of clustering extensions

	The output file (``kmedoids.xlsx``) contains the clustering result by K-medoid clustering algorithm.

3. The details of manually selecting extensions

	The output file (``extension selection steps.xlsx``) contains the process of selecting representative extensions with reasons provided.

4. Installation packages of extensions

	All candidate extensions (representative + discarded) are presented in folder crx. The installation packages of extensions are named by the extension ids. The folder name under crx (e.g., 1 and 2) is related to the cluter. For example, the selected extensions that are clutered to cluster 1, can be found in crx -> 1.
	
5. Raw data

	Our measurements to the browser performance can be found under the folder - raw performance data. ``Free.txt`` contains the measurements for the extension-free mode. The file ``full.txt`` contains the measurements for the fully loaded mode.
	
6. model results

	Our linear mixed effects models can be found in the folder - saved models. To load the model, ``robustlmm`` function in R is required. Run ``readRDS("page load time.rds")`` to load the model in local.
 
