# Financial Distress for Individuals

Given the definition of Financial Distress, while is certainly a well known parameter for companies, the challenge for you is to propose how you would go about building and model for Prediction of Financial Distress for Individuals, giving them a score and productising it via an API.


1. Assuming you have access to banking data (transactions) and also from any other source: telco, personal data, etc. (including other digital platforms), identify features/parameters (not extensively but most important ones to consider) to be part of your proposed solution.

   * **Transaction data**: debit/credit information. This should be the most important feature that shows the key financial information of the individual.
debit: for all amounts above a certain threshold, find fix and variable expenditures over a period of time. 
credit: average amount credited in the account
avg (credit-debit) amount, and net values annually

   * Personal wealth (assets, cash, etc.)
   * Financial literacy indicators (eg: exposure to stock investments?)
   * Demographic information. This can include information about the job/business, location, age, etc. Some critical information might be contained in this data. 
   

2. Which algorithm(s) would you propose

    The problem can be formulated in two formats:

    * **Supervised learning approach:** The problem can be formulated as a binary classification problem, and the output of the probabilities (between 0 to 1) can be transformed into a score that indicates the likeliness of financial distress. Simpler linear models like logistic regression can be tested, and more advanced deep learning methods can also be considered. The output label can be extracted from the data using many methods, one of which could be to categorize an individual in financial distress if the (credit-debit) amount is negative for a certain number of rolling months. 
  
    * **Unsupervised learning approach:** Clustering techniques can be used to group similar customers in multiple categories for different levels of financial distress. The different (credit-debit) values can be used to understand the ideal number of groups. The individuals can then be mapped to these existing clusters to see the proximity to the cluster, and the (distance from cluster center * weight of cluster) can be used as the score. 
  

3. How would you build and train your model.

   * Analysis: The first step would be to analyze the data using the standard Python toolkit like numpy, pandas, matplotlib, etc.
   * Pre-processing: The second step would be to create a pre-processing module that prepares the data for training. This module will also be required for productionizing the model as the data needs to be prepped for generating the predictions. 
   * Training: This step would involve creating train, test, validation sets and testing the models and parameters. The final model will be saved and versioned. MLFlow can be used for model versioning, and specific libraries would depend on the algorithm.
   * Evaluation: An evaluation pipeline needs to be defined that quantatively and qualitatively evaluates the performance of the model on the fix/input test sets. 

4. How would you productise the predictive financial distress model in order to consume it and update it (real time) with more data.

   A flask API can be created that loads up the latest version of the model, processes the input data from a new individual (as an input parameter), and generates prediction through the model. This prediction and the requisite information is sent as a response from the API, or stored in the DB from where it can be read by the consuming service. Here's a schematic of how it would work:
   ![Training pipeline](/IMG_0879.jpg)
   
   A weekly scheduler can use the saved data to update the model with the latest data and store the improved model. A rough schematic of the process:
   ![Retraining pipeline](/IMG_0880.jpg)

5. Which part is the most challenging? 

   I believe that defining the output of the problem would the hardest challenge. This would include determining which individual is considered to be in financial distress, and how that would be determined. The determination of the level of financial distress, and the time period to consider for the evalution would be hard to establish without experimentation and feedback.

6. How do you think this is gonna impact people's lives? 
   
   The determination of a financial distress score can help individuals determine if they have good financial health or if corrective steps are necessitated. It can also help people determine what finacial changes can negatively impact their financial health. Additionally, this information can be used by institutions to gauge credit worthiness, upcoming defaults, general finances across the market, and so on. 
