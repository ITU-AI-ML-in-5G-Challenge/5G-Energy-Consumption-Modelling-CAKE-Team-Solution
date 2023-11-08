# aiml-for-5g-energy-consumption-modelling_Team-CAKE
This is the repo of Team CAKE in AI/ML for 5G-Energy Consumption Modelling by ITU AI/ML in 5G Challenge

Set up folders
- CAKE:  Root path
	- BestModel: Saved best training model
		- best_w1.pth: Best model w.r.t w=1 weight 
		- best_w5.pth: Best model w.r.t w=5 weight 
	- EnergyContest: Raw data files
	- w1.ipynb: w.r.t w=1, data preprocessing, model training and evaluation when w=1 
	- w5.ipynb: w.r.t w=5, data preprocessing, model training and evaluation when w=5
	- unite.ipynb: Merge prediction value under w=1 and w=5
	- model_best_w1.pth: Best model w.r.t w=1, a.k.a model with mininal train loss during training 
	- model_last_w1.pth: Last model w.r.t w=1, a.k.a model after all epochs are trained 
	- model_best_w5.pth: Best model w.r.t w=5, a.k.a model with mininal train loss during training
	- model_last_w5.pth: Last model w.r.t w=5, a.k.a model after all epochs are trained
	- power_consumption_prediction_best.csv: Saved best prediction values, but seed had not been set during this time training, thus it may differ a little from reproduction
	- power_consumption_prediction_new.csv: Merged prediction values under w=1 and w=5 
	- power_consumption_prediction_w1.csv: Prediction values under w=1
	- power_consumption_prediction_w5.csv: Prediction values under w=5

Where file is save
Attention: All paths in code are set to be relative path, thus there is no need to change path for running code
w1.ipynb: 
	- Read four raw data files (BSinfo.csv, CLdata.csv, ECdata.csv, power_consumption_prediction.csv) under "BestModel" folder, with path "./BestModel/BSinfo.csv", "./BestModel/CLdata.csv", "./BestModel/ECdata.csv", "./BestModel/power_consumption_prediction.csv"
	- Output prediction values under w=1 in "power_consumption_prediction_w1.csv", saved under root path "./power_consumption_prediction_w1.csv"
	- Output best model "model_best_w1.pth" and last model "model_last_w1.pth" under w=1, saved under root path
w5.ipynb: 
	- Read four raw data files (BSinfo.csv, CLdata.csv, ECdata.csv, power_consumption_prediction.csv) under "BestModel" folder, with path "./BestModel/BSinfo.csv", "./BestModel/CLdata.csv", "./BestModel/ECdata.csv", "./BestModel/power_consumption_prediction.csv"
	- Output prediction values under w=5 in "power_consumption_prediction_w5.csv", saved under root path "./power_consumption_prediction_w5.csv"
	- Output best model "model_best_w5.pth" and last model "model_last_w5.pth" under w=5, saved under root path
unite.ipynb: 
	- Read prediction values under root path "./power_consumption_prediction_w1.csv" for w=1 and "./power_consumption_prediction_w5.csv" for w=5
	- Output merged prediction values for both w=1 and w=5 in "power_consumption_prediction_new.csv", under "./power_consumption_prediction_new.csv", this file is the final prediction values file

Order in which to run code:
Step1: Run all w1.ipynb, obtain power_consumption_prediction_w1.csv (set evaluate_flag to be 1 to load from best model then evaluation, else value will evaluate from model trained from scratch), and save to root path
Step2: Run all w5.ipynb, obtain power_consumption_prediction_w5.csv (set evaluate_flag to be 1 to load from best model then evaluation, else value will evaluate from model trained from scratch), and save to root path
Step3: Run all unite.ipynb, obtain power_consumption_prediction_new.csv, and save to root path.
(Run all means run the blocks in the notebook one by one)

Features used: 
w.r.t w=1, merge features of cell0 at the same BS and Time, and discard data from cell1, cell2, and cell3. One hot the features 'Mode', 'RUType', 'Antennas', 'Frequency', and drop the columns if its variation is 0.
w.r.t w=5, merge all features at the same BS and Time, including entries from cell0, cell1, and cell2. One hot the features 'Mode','RUType','Antennas','Bandwidth','Frequency', and drop the columns if its variation is 0. Finally, append 1) the mean, sum of loads from different cells, and 2) the mean, sum of ESMode from different cells as new features.

Hardware conditions: 
CPU:  Intel(R) Xeon(R) Silver 4210R CPU @ 2.40GHz
GPU:  NVIDIA GeForce GTX 3090
CUDA Version:  11.8

Software settings: 
conda version:  4.10.3

Runtime:
When w=1, need to run until train loss less than 0.4 which will take about 3 hours
When w=5, need to run until train loss less than 1.1 which will take about 20 hours
