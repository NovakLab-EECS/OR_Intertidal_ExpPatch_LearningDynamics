# Fall 2021-Spring 2022 Development

[Link to Github Repository](https://github.com/montsam/OR_Intertidal_ExpPatch_LearningDynamics/tree/main/CodeFreeze2022)

## Problem Statement
This project aims to create an accurate and comprehensible model to describe and predict population dynamics for species in the Oregon marine intertidal using a novel machine learning technique known as symbolic regression. Ideally, this model can be applied to describe other ecosystems as an alternative to traditional methods of characterizing species interactions.

## Required Software
As the development team was already using a group google drive for documentation coordination, they decided to use [Google Colaboratory](https://research.google.com/colaboratory/faq.html), an in-browser python notebook capable of allowing multiple programmers to work concurrently on python code. Attached below is a link to a google drive containing all documentation and Colab notebooks used to run the tests. 
[Link to team drive](https://drive.google.com/drive/folders/1nQV2U_Dj1jwzslvPh9jWLsub_tL8sly2?usp=sharing) (must access with an OSU email).
#### Google Drive Layout
The linked drive houses two directories; *Documentation* and *Colab Notebooks*. The first directory in the shared drive houses findings over the course of the project along with the datasets used while the second houses the two notebooks we used to run our Symbolic Regression Models.

#### Libraries
All required libraries are included in the imports section of the Google Colaboratory notebooks with some notable libraries listed below:
 - [gplearn](https://gplearn.readthedocs.io/en/stable/) was the library used to run the symbolic regression analysis. A more in depth overview of this software and how it functions is included later in this document.
 - [sklearn](https://scikit-learn.org/stable/) was used for fine tuning parameters via their included grid search package.

## How to Run
The process to run our code is fairly simple as our project was more about data manipulation and hyperparameter optimization rather than large codebases. A numbered list of steps to run either colab notebook is included below.

 1. Ensure you have the ability to view/edit Google Colaboratory Notebooks by opening either of the two found in the "Colab Notebooks" section of the shared drive
 2. Run the first code block up until you are prompted to mount your google drive (this is needed to allow colab to find the uploaded datasets)
 3. From here, you will need to edit the file paths found in the dataset uploading section of the notebooks to match your own drive. A link to a comprehensive guide to accomplishing this is here: [Link to dataset tutorial](https://docs.google.com/presentation/d/1As5lJr7xMapC2TLe5i-oFwj3m0TqanhaZU-31tfY-X8/edit?usp=sharing)
 4. Once the datasets are linked, the rest of the code can be ran. Follow the comments within the notebook to gain better understanding into the blocks

## Features
 - [x] Colab notebook using symbolic regression to predict growth rate
	 - [x] Includes visualizations for datasets imported
	 - [ ] Uses grid search to find optimal parameters 
	 - [x] Includes visualizations for equations generated
	 - [x] Simplifies generated equation if possible
 - [x] Colab notebook using symbolic regression to predict feeding rate
	- [x] Includes visualizations for datasets imported
	- [x] Uses grid search to find optimal parameters 
	- [ ] Includes visualizations for equations generated
	- [x] Simplifies generated equation if possible


#### Expansion Opportunities 
Much of this project was spent understanding the complex interactions of gplearn and how it interacted with the provided datasets. For a complete list of our findings over the course of the project, refer to the *Documentation* directory in the attached drive. The two notable suggestions we have for the next team continuing development are

 1. Migrate away from colab into local machines. Colab was an excellent way to begin work, allowing us begin optimizing the models immediately in a familiar environment; however this simplicity came at a tradeoff of frequent timeouts and parameter limitations. We recommend using a Jupyter notebook or connecting the colab notebooks to a local runtime to avoid timeouts and use your own machines processors.
 2. Run the models by making use of the Warm_Start Parameter in the Symbolic Regressor, and limit the generation count to smaller numbers. Rather than running one 8 hour 5000 generation execution, running many 100 generation (possibly in a for loop or similar structure) executions will allow the models to create more equations to provide further insight into what parameters need tweaking. This has the added benefit of being more resilient against crashes and timeouts.

