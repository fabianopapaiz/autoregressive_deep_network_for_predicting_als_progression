# Autoregressive Multi-Step Multi-Output Deep Neural Network for Predicting Amyotrophic Lateral Sclerosis Progression


This study is the first to employ this approach to ALS prognosis to predict the functional decline over time. We extracted static and temporal features from the Pooled Resource Open-Access ALS Clinical Trials (PRO-ACT) database. We developed and evaluated deep learning models using the Gated Recurrent Unit and Long Short-Term Memory algorithms. Our approach outperformed previous works with a significantly smaller set of input features, thus demonstrating greater effectiveness. With the promising results obtained, our approach could aid physicians in devising personalized treatment and resource planning or serve as an inclusion/exclusion criterion in clinical trials.  
The results of this work have been published in the research article "Autoregressive Multi-Step Multi-Output Deep Neural Network for Predicting Amyotrophic Lateral Sclerosis Progression" (Papaiz et al., 2024).


**If you use this code for your research please cite this paper:**

> Papaiz F, Dourado MET, Valentim RAdM, dos Santos JPQ, Fernandes FRdS, de Morais AHF, Correia FB, Arrais JP. Autoregressive Multi-Step Multi-Output Deep Neural Network for Predicting Amyotrophic Lateral Sclerosis Progression. 2024.
   
[LICENSE](LICENSE)

---
For those wanting to try it out, this is what you need:
1) A working version of Python (version 3.9+) and jupyter-notebook.

---

2) Install the following Python packages:
    - numpy (1.23.5)
    - pandas (1.5.3)
    - matplotlib (3.7.0)
    - seaborn (0.12.2)
    - scikit-learn (1.2.1)
    - imbalanced-learn (0.10.1)
    - shap (0.41.0) 

---

3) Download the patient data analyzed from the Pooled Resource Open-Access ALS Clinical Trials (PRO-ACT) website (https://ncri1.partners.org/ProACT)
    - Register and log in to the website
    - Access the `Data` menu and download the `ALL FORMS` dataset
    - Extract the zipped data file into the `01_raw_data` folder
    - The `01_raw_data` folder will contain the following CSV files
      
      ![raw_data_folder](https://github.com/fabianopapaiz/als_prognosis_using_ensemble_imbalance/assets/16102250/dc9c533d-8152-44f0-b0f4-5b9112f34e04)

---
      
4) Perform the Extract-Load-Transform (ETL) step:    
    - Start the `jupyter-notebook` environment 
    - Open and execute all code of the `02.01 - Preprocess raw data.ipynb` file, which is inside the `02_ETL` folder
    - After execution, the preprocessed data will be saved in the `03_preprocessed_data` and `04_data_to_analyze` folders

    ![preprocessed data](https://github.com/fabianopapaiz/als_prognosis_using_ensemble_imbalance/assets/16102250/b86b4ecd-1f3d-44b4-aa54-ceb1b8860f3f)

---

5) Perform the Machine Learning (ML) pipeline:
    - Execute the python program ```exec_grid_search_both_scenarios.py``` in the `05_Train_Validate_Models` folder
    - This program will:
        - Split the dataset into _Training_ and _Validation_ subsets 
        - Train and validate the ML models for both scenarios (_Single-Model_ and _Ensemble-Imbalance_)
           - NOTE: It can take a long time to accomplish (even days).
        - Save the performance results into CSV files in the `05_Train_Validate_Models/exec_results` folder
             
    - Pipeline Overview:

      ![overall](https://github.com/fabianopapaiz/autoregressive_deep_network_for_predicting_als_progression/assets/16102250/10559c84-9b84-460d-91ca-132dab0124d4)



    - Validation performance obtained by each scenario and algorithm:
  
      ![best_performance_by_model_ALSFRS_Total](https://github.com/fabianopapaiz/autoregressive_deep_network_for_predicting_als_progression/assets/16102250/b15c9e02-633b-4d65-ad73-c15555f3bf95)


    - Best deep model architecture:

      ![rnn](https://github.com/fabianopapaiz/autoregressive_deep_network_for_predicting_als_progression/assets/16102250/87baaf73-c88e-4d04-bf23-5ab4ec8c4e7d)

          
    - Individualized predictions:

      ![patient_example_2](https://github.com/fabianopapaiz/autoregressive_deep_network_for_predicting_als_progression/assets/16102250/c7c180ef-d15e-4bd2-a983-287b80206060)



7) Grid-Search hyperparameters used for each algorithm.

![grid-search-params](https://github.com/fabianopapaiz/ensemble_imbalance_model_for_als_prognosis/assets/16102250/8ed50d34-ff82-43c7-8364-b51d9ffbff8b)


---

8) Best models' hyperparameters

![best-model-params](https://github.com/fabianopapaiz/ensemble_imbalance_model_for_als_prognosis/assets/16102250/2d00db54-ddd3-4001-9193-15fa1ac12ca5)

---

9) Additional Information:

   [Exploratory Data Analysis](https://github.com/fabianopapaiz/ensemble_imbalance_model_for_als_prognosis/files/12899208/additional_info.pdf)


---
Finally, please let us know if you have any comments or suggestions, or if you have questions about the code or the procedure (correspondence e-mail: `fabianopapaiz at gmail dot com`). 


