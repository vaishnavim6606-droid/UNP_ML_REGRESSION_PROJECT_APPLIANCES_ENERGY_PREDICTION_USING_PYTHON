# UNP_ML_REGRESSION_PROJECT_APPLIANCES_ENERGY_PREDICTION_USING_PYTHON
This project was completed as part of the United Network of Professionals (UNP) Machine Learning Academic Internship Program.

Appliances Energy Prediction using Machine Learning

Team (Group 7): Vaishnavi · K Narayan · Neha Byroju · G Hasini

Predicts household appliance energy consumption (in Wh) from indoor sensor readings, outdoor weather and time-of-day features. Seven regression models and an Artificial Neural Network (ANN) are compared across five train–test splits, tuned with GridSearchCV, and evaluated in two experiments: without and with VIF-based feature selection.

Dataset
Source: Appliances Energy Prediciton.xlsx (file name as spelled in the notebook), 19,735 records at 10-minute intervals, 29 original columns
Target: Appliances (mean 97.69, median 60, max 1,080)
After pre-processing: dropped rv1/rv2, derived Month and Hour from date, dropped date, leaving 27 input features + the target
No missing values or duplicate rows; outliers were inspected (2,138 Appliances values fall outside the IQR fences) but not removed
Features: lights, indoor temperature T1–T9, indoor humidity RH_1–RH_9, T_out, RH_out, Press_mm_hg, Windspeed, Visibility, Tdewpoint, Month, Hour
Workflow
Pre-processing: missing/duplicate/constant-column checks, dropped rv1 and rv2, created Month and Hour
EDA: hourly consumption bar chart, histograms, box plots, line plots and a correlation heatmap
ML models: Linear Regression, KNN, Decision Tree, Random Forest, Gradient Boosting, XGBoost, SVR
Pipeline: train–test split → StandardScaler (fitted on training data) → fit → evaluate with R², RMSE, MAE and MAPE
Splits: 60:40, 65:35, 70:30, 75:25, 80:20 (random_state = 42)
ANN: 10 Keras configurations (Adam vs SGD, varying depth and width) with EarlyStopping
Hyperparameter tuning: GridSearchCV (5-fold CV, scored on R²) for all seven models on the 80:20 split
Feature selection (VIF): removed multicollinear features one at a time, highest VIF first (27 → 19 features), then repeated the whole analysis and compared the two experiments
Key EDA Insights
Average consumption is lowest overnight and peaks around hour 18.
Individual features correlate only weakly with consumption. The strongest are Hour (0.22) and lights (0.20); RH_out is the strongest negative (−0.15). Appliance usage is therefore only moderately predictable.
Results (80:20 split unless noted)
Without VIF (27 features)
Model	R²	RMSE	MAE	MAPE (%)
KNN (GridSearchCV)	0.6238	58.29	26.54	25.52
Random Forest (GridSearchCV)	0.5975	60.29	29.26	29.86
XGBoost (best untuned, 75:25)	0.5475	67.04	33.28	34.70
Best ANN (256-128-64-32, Adam)	0.5162	66.10	31.59	31.46
With VIF (19 features)
Model	R²	RMSE	MAE	MAPE (%)
KNN (GridSearchCV)	0.5780	64.99	29.62	28.03
Random Forest (GridSearchCV)	0.5624	66.17	30.97	31.20
Random Forest (best untuned)	0.5451	67.47	31.95	32.51
Best ANN (128-64-32-16, Adam)	0.4870	71.21	33.85	32.69

VIF removed these 8 features: T_out, T9, T2, T6, RH_4, T7, T1, Month (highest VIF fell from 155.58 to 9.40).

Findings
Tuned KNN was the best model in both experiments, beating the tree ensembles and every ANN.
XGBoost and Random Forest were the two best untuned models at every split.
GridSearchCV lifted almost every model; the largest gain was SVR (R² 0.04 → 0.31 without VIF).
Adam outperformed SGD for the four larger ANN architectures in both experiments.
VIF did not improve accuracy: the best untuned, tuned and ANN results were all equal or lower with VIF. It does give a simpler 19-feature set at similar untuned accuracy for Random Forest and XGBoost.
Linear Regression and untuned SVR were the weakest models.
Note: the two ANN experiments used different architectures, batch sizes and seeds, so their comparison is indicative rather than a pure VIF effect.
Future Applications

Smart-home energy monitoring, hourly demand prediction, energy optimization and home energy management dashboards.

Tech Stack

Python, pandas, NumPy, scikit-learn, XGBoost, TensorFlow/Keras, statsmodels, Matplotlib, Seaborn

Code Link (With VIF) : https://drive.google.com/file/d/1kF3lMdGNfvSRh_JtbbfkOH84_jT38yT-/view?usp=drive_link

Code Link (Without VIF) : https://drive.google.com/file/d/10JRWbZv5nak6BWFTbu4MHGD5G9IvWFs2/view?usp=drive_link

PPT Link : https://docs.google.com/presentation/d/1lN7yA1DmQlQWWmInVyCao9IwNl59Lx-b/edit?usp=drive_link&ouid=113382930934840677528&rtpof=true&sd=true

Acknowledgements

Thanks to UNP Education (United Network of Professionals) for the internship opportunity and guidance for this project.
