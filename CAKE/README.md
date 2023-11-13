# aiml-for-5g-energy-consumption-modelling_Team-CAKE
This is the repo of Team CAKE in AI/ML for 5G-Energy Consumption Modelling by ITU AI/ML in 5G Challenge

### Set up folders
- CAKE:  Root path
	- BestModel: Saved best training model
		- model_best_TestBS-in-TrainingSet.pth: Best model w.r.t test BS in training set weight 
		- model_best_TestBS-not-in-TrainingSet.pth: Best model w.r.t test BS not in training set weight 
	- EnergyContest: Raw data files
	- TestBS_in_TrainingSet.ipynb: w.r.t test BS in training set, data preprocessing, model training and evaluation when test BS in training set 
	- TestBS_not_in_TrainingSet.ipynb: w.r.t test BS not in training set, data preprocessing, model training and evaluation when test BS not in training set
	- unite.ipynb: Merge prediction value under test BS in training set and test BS not in training set
	- model_TestBS-in-TrainingSet.pth: Last model w.r.t test BS in training set, a.k.a model after all epochs are trained 
	- model_TestBS-not-in-TrainingSet.pth: Last model w.r.t test BS not in training set, a.k.a model after all epochs are trained
	- power_consumption_prediction_best.csv: Saved best prediction values, but seed had not been set during this time training, thus it may differ a little from reproduction
	- power_consumption_prediction_new.csv: Merged prediction values under test BS in training set and test BS not in training set 
	- power_consumption_prediction_TestBS-in-TrainingSet.csv: Prediction values under test BS in training set
	- power_consumption_prediction_TestBS-not-in-TrainingSet.csv: Prediction values under test BS not in training set
	- model_TestBS-in-TrainingSet_progress.txt: Loss and epoch duration during training w.r.t test BS in training set
	- model_TestBS-not-in-TrainingSet_progress.txt: Loss and epoch duration during training w.r.t test BS not in training set
	- visualize.ipynb: Visualize changes in loss and epoch duration during training

### Where file is save  
**Attention**: All paths in code are set to be relative path, thus there is no need to change path for running code  
- TestBS_in_TrainingSet.ipynb: 
	- Read four raw data files (BSinfo.csv, CLdata.csv, ECdata.csv, power_consumption_prediction.csv) under "BestModel" folder, with path "./BestModel/BSinfo.csv", "./BestModel/CLdata.csv", "./BestModel/ECdata.csv", "./BestModel/power_consumption_prediction.csv"
	- Output prediction values under test BS in training set in "power_consumption_prediction_TestBS-in-TrainingSet.csv", saved under root path "./power_consumption_prediction_TestBS-in-TrainingSet.csv"
	- Output last model "model_TestBS-in-TrainingSet.pth" under test BS in training set, saved under root path
- TestBS_not_in_TrainingSet.ipynb: 
	- Read four raw data files (BSinfo.csv, CLdata.csv, ECdata.csv, power_consumption_prediction.csv) under "BestModel" folder, with path "./BestModel/BSinfo.csv", "./BestModel/CLdata.csv", "./BestModel/ECdata.csv", "./BestModel/power_consumption_prediction.csv"
	- Output prediction values under test BS not in training set in "power_consumption_prediction_TestBS-not-in-TrainingSet.csv", saved under root path "./power_consumption_prediction_TestBS-not-in-TrainingSet.csv"
	- Output last model "model_TestBS-not-in-TrainingSet.pth" under test BS not in training set, saved under root path
- unite.ipynb: 
	- Read prediction values under root path "./power_consumption_prediction_TestBS-in-TrainingSet.csv" for test BS in training set and "./power_consumption_prediction_TestBS-not-in-TrainingSet.csv" for test BS not in training set
	- Output merged prediction values for both test BS in training set and test BS not in training set in "power_consumption_prediction_new.csv", under "./power_consumption_prediction_new.csv", this file is the final prediction values file

### Order in which to run code:  
Step1: Run all TestBS_in_TrainingSet.ipynb, obtain power_consumption_prediction_TestBS-in-TrainingSet.csv (set evaluate_flag to be 1 to load from best model then evaluation, else value will evaluate from model trained from scratch), and save to root path  
Step2: Run all TestBS_not_in_TrainingSet.ipynb, obtain power_consumption_prediction_TestBS-not-in-TrainingSet.csv (set evaluate_flag to be 1 to load from best model then evaluation, else value will evaluate from model trained from scratch), and save to root path  
Step3: Run all unite.ipynb, obtain power_consumption_prediction_new.csv, and save to root path.  
Step4(Not necessary): Run all visualize.ipynb, changes in loss and epoch duration during the training process can be observed.  
(**Run all** means run the blocks in the notebook one by one)

### Features used:  
Merge all features at the same BS and Time, including entries from cell0, cell1, and cell2. One hot the features 'Mode','RUType','Antennas','Bandwidth','Frequency', and drop the columns if its variation is 0. Finally, append 1) the mean, sum of loads from different cells, and 2) the mean, sum of ESMode from different cells as new features.

### Hardware conditions: 
CPU:  Intel(R) Xeon(R) Silver 4210R CPU @ 2.40GHz  
GPU:  NVIDIA GeForce GTX 3090  
CUDA Version:  11.8  

### Software settings: 
conda version:  4.10.3

### Runtime:
When test BS in training set, need to run until train loss less than 0.4 which will take about 2 hours  
When test BS not in training set, need to run 150 epochs which will take about 1 hour
