Oz Kilic  
Carleton University  
COMP 5118 Project

# Successful Pass Prediction in Football Using Deep Learning

In this course project, I trained a deep learning model to predict a pass position's success in football (soccer). The model uses a combination of position images and features. For more information, please refer to the report (submitted separately). The trained model is later used to make decisions in a specific pass position. While the model's predictions are decent (obtaining a macro-weighted F1 score of 0.7595), suggestions obtained from the model are heavily biased towards historically more successful directions and techniques, requiring further attention. The fact the actual reward (scoring a goal) is delayed means we need reinforcement learning for the optimization part (which would be a course project by itself). My project was more about the prediction and this part was more of an afterthought anyway. The code is not as clean and documented as I normally do here.

## Running the code

### Preparations

To install the necessary libraries, you can run `pip install -r requirements.txt` in the project folder.

This project uses [StatsBomb's soccer datasets](https://github.com/statsbomb/open-data). While the event dataset is pulled as needed, the 360 dataset files must be present in a folder named "360" in the project folder.

All codes are in the Jupyter Notebook format.

### Data processing

Run the code blocks in `data_processor.ipynb` in order. By default, it requires having the 360 dataset in a folder named "360" in the project folder. However, dataset directory and export file/folder names can be changed from the code. You can also make changes on the code to change the number of discretized angle groups for passes and so on.

Processing requires processing the position data and then processing the event data. Processing the position data takes very long and the folder size can be large (25+ GB for 100 matches). After finding the relevant positions and processing them, the code finds the event data that correspond to these positions and processes them to be used later.

While the folder exists in the repository, I am providing only a single match's position tensors in case you want to examine the tensors yourself. The processed event dataset is entirely shared.

### Model training

Run the code blocks in `model.ipynb` in order. This notebook filters the previously processed dataset, creates dataset and dataloader objects, creates the model, applies hyperparameter search, trains the model, and tests it.

Without CUDA, model training may take a long time. Note that I also provided the model I mention in my report.

### Pass optimization

Run the code blocks in `pass_optimization.ipynb` in order. This notebook uses all relevant data to make suggestions about which decision could yield a better result. After doing some preliminary analyses and data visualization, the notebook separates the dataset into successful and unsuccessful passes. For each type, it tries to find the pass height and pass angle that would make the pass successful, and visualizes them using Sankey diagrams.

### Other

Please contact me if you encounter a problem.
