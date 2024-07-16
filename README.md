# Autoregressive Multi-Step Multi-Output Deep Neural Network for Predicting Amyotrophic Lateral Sclerosis Progression


This study is the first to employ this approach to ALS prognosis to predict the functional decline over time. We extracted static and temporal features from the Pooled Resource Open-Access ALS Clinical Trials (PRO-ACT) database. We developed and evaluated deep learning models using the Gated Recurrent Unit and Long Short-Term Memory algorithms. Our approach outperformed previous works with a significantly smaller set of input features, thus demonstrating greater effectiveness. With the promising results obtained, our approach could aid physicians in devising personalized treatment and resource planning or serve as an inclusion/exclusion criterion in clinical trials.  
The results of this work have been published in the research article "Autoregressive Multi-Step Multi-Output Deep Neural Network for Predicting Amyotrophic Lateral Sclerosis Progression" (Papaiz et al., 2024).


**If you use this code for your research please cite this paper:**

> Papaiz F, Dourado MET, Valentim RAdM, dos Santos JPQ, Fernandes FRdS, de Morais AHF, Correia FB, Arrais JP. Autoregressive Multi-Step Multi-Output Deep Neural Network for Predicting Amyotrophic Lateral Sclerosis Progression. 2024.
   
[LICENSE](LICENSE)

---
For those wanting to try it out, this is what you need:
1) #### A working version of Python (version 3.9+) and jupyter-notebook.

---

2) #### Install the following Python packages: </h3>

    - numpy (1.23.5)
    - pandas (2.1.1)
    - matplotlib (3.8.0)
    - seaborn (0.13)
    - scikit-learn (1.3.2)
    - TensorFlow (2.14)
    - notebook (6.5.5)

---

3) #### Download the patient data analyzed from the Pooled Resource Open-Access ALS Clinical Trials (PRO-ACT) website ([https://ncri1.partners.org/ProACT](https://ncri1.partners.org/ProACT))
   
    - Register and log in to the website
    - Access the `Data` menu and download the `ALL FORMS` dataset
    - Extract the zipped data file into the `01_raw_data` folder
    - The `01_raw_data` folder will contain the following CSV files

     ![Screenshot 2024-07-16 08:20:20](https://github.com/user-attachments/assets/ac9848ad-7f55-4dff-bd93-7b1defbf5a81)

      
---
      
4) #### Perform the Extract-Load-Transform (ETL) step:    
    - Start the `jupyter-notebook` environment 
    - Open and execute all code of the `02.01 - Preprocess raw data.ipynb` file, which is inside the `02_ETL` folder
    - After execution, the preprocessed data will be saved in the `03_preprocessed_data`, `04_data_to_analyze`, and `05_data_as_time_series` folders

    ![Screenshot 2024-07-16 08:24:33](https://github.com/user-attachments/assets/e1e9534c-a41f-4e8a-ab51-5e82ba480611)


---
      
5) #### Temporal data file
    - The file `data_as_time_series_15m_data_Only_ALSFRS.csv` contains all the temporal data analyzed in this study. It contains the patient data for all features (`n=22`) and all time steps (from `0` up to `15`)

    ![Screenshot 2024-07-16 08:29:14](https://github.com/user-attachments/assets/34d5c880-b2d5-4f1a-97b8-5f9b65c8102c)


    - Features analyzed:

        ![Screenshot 2024-07-16 08:33:39](https://github.com/user-attachments/assets/d7a55da2-7394-450e-b87c-a58da4e3961e)

      

---

6) #### Perform the Machine Learning (ML) pipeline:
   
    6.1) Split the dataset into _Training_ (80%) and _Validation_ (20%) subsets
   
    6.2) Utilize the _Training_ subset to create the matrices **_X_**'s (1) comprising information about the variation of all features over time for each patient, where _f_ = 1, 2, ..., 22 (features) and _t_ = 0, 1, ..., 15 (time steps)

      ![Screenshot 2024-07-16 08:40:15](https://github.com/user-attachments/assets/a7d5f6f5-4428-4f7d-ac64-0b9507d80473)

   
   
    6.3) Generate the learning instances from the matrices **_X_**'s for each time step. Use a sliding window with size 4 and shifted by 1.
  
      ![Screenshot 2024-07-16 08:44:56](https://github.com/user-attachments/assets/f512bf2a-9dc4-4089-ad21-ad820b18c20a)

    
             
    6.4) Develop and train GRU and LSTM models using the 5-fold Cross Validation strategy. To prevent overfitting, you can shuffle the learning instances before training and employ the following strategies: 5-fold Cross-Validation (CV), early stopping, regularization, and drop-out. Evaluate several combinations of hyperparameters using the grid-search strategy. Our hyperparameter search space included the number of hidden layers, the model depth (neurons), the initial learning rate, regularization, and the unidirectional and bidirectional architectures.

      ![Screenshot 2024-07-16 08:55:50](https://github.com/user-attachments/assets/5e31ef36-dc45-4cf3-a620-cf9274a1c938)


    6.5) Use the Autoregressive Multi-Step Multi-Output approach to evaluate the models using 3-month data to predict the next 12 months, comparing the predicted and actual values. The metrics utilized were **RMSE** and **R<sup>2</sup>**.

      ![Screenshot 2024-07-16 09:02:47](https://github.com/user-attachments/assets/a58ee2cd-1e7b-4599-b898-7db92b793de9)




    6.6)- **Pipeline Overview:**

      ![overall](https://github.com/fabianopapaiz/autoregressive_deep_network_for_predicting_als_progression/assets/16102250/10559c84-9b84-460d-91ca-132dab0124d4)


---

7) #### Best validation performance obtained by each algorithm (GRU and LSTM):
  
      ![best_performance_by_model_ALSFRS_Total](https://github.com/fabianopapaiz/autoregressive_deep_network_for_predicting_als_progression/assets/16102250/b15c9e02-633b-4d65-ad73-c15555f3bf95)


---

8) #### Best deep learning model architecture (GRU):

      ![rnn](https://github.com/fabianopapaiz/autoregressive_deep_network_for_predicting_als_progression/assets/16102250/87baaf73-c88e-4d04-bf23-5ab4ec8c4e7d)

          
---

9) #### Grid-Search hyperparameters used for each algorithm.

   - Drop-out rates: 10%, 20%, 30%, 35%, 40%, 45%, and 50%
   
   - Regularizers:
      - Types: LASSO, Ridge, and ElasticNet
      - Values: 0.1, 0.01, 0.001
    
   - Initial learning rate: 10<sup>-7</sup>

   - RNN architectures: unidirectional and bidirectional
     
   - Number of neurons and hidden layers:
       - [64]      
       - [64, 64]      
       - [64, 64, 64]      
       - [128]      
       - [128, 128]      
       - [128, 128, 128]      
       - [256]
       - [256, 256]       
       - [256, 256, 256]
       - [512]       
       - [512, 512]       
       - [512, 512, 512]       
       - [1024]       
       - [1024, 1024]       
       - [1024, 1024, 1024]       
       - [2048]       
       - [2048, 2048]       
       - [2048, 2048, 2048]       



---

10) #### Best deep learning model's hyperparameters (GRU):

   - Drop-out rate: 35%
   
   - Regularizer: Ridge = 0.001
    
   - RNN architecture: bidirectional
     
   - Number of neurons and hidden layers: [1024, 1024]


---

11) #### Individualized predictions using a patient from the _Testing_ subset:

      ![patient_example_2](https://github.com/fabianopapaiz/autoregressive_deep_network_for_predicting_als_progression/assets/16102250/c7c180ef-d15e-4bd2-a983-287b80206060)


---

### Finally, please let us know if you have any comments or suggestions, or if you have questions about the code or the procedure (correspondence e-mail: `fabianopapaiz at gmail dot com`).


