# Browser In The Middle - BitM Phishing Detection using Machine Learning


## Objective
The objective of this study is to perform an in-depth performance evaluation of various machine learning algorithms to identify the most effective classifier for detecting Browser-in-the-Middle (BitM) phishing attacks. By analyzing packet captures from safe and malicious scenarios using Wireshark, the study aims to develop a novel empirical method for detecting BitM phishing attacks through supervised machine learning, focusing on distinguishing between legitimate and compromised connections based on network traffic.

## Data Collection And Preprocessing 
The Browser-in-the-Middle (BitM) architecture was replicated on a local machine using VirtualBox (version 6.7.10) with two Ubuntu 22.4 LTS instances. The setup involved three distinct machines: a victim machine, an attacker’s machine, and an intended server. Wireshark (version 4.0.9) was installed on the victim machine to intercept and capture network traffic, producing pcap files for analysis. Two types of traffic were generated: safe and malicious.

Malicious traffic was captured when the victim clicked a phishing link, which created a remote connection to the intended server through the attacker’s machine. In contrast, safe traffic was captured when the victim connected directly to the intended server without any malicious intervention.

The pcap files revealed different attributes for safe and malicious traffic. Specifically, data packets were captured in total—60% were identified as malicious and 40% as safe. The next step in the analysis involves importing these pcap files into Google Collaboratory, where the 'tshark' tool used to process and analyze the network packet data to differentiate between the two types of traffic by labeling them into a csv file.



*Here is the final csv [![Dataset](https://img.shields.io/badge/Dataset-BitM_Phishing-indigo%09%09?logo=github)
](https://github.com/farhanshahriyar-cse/BitM_Browser-In-The-Middle-Phishing-Detection-using-Machine-Learning/tree/f984f930b06d1a10e8dd80116ba57002a6478381/Datasets)*


These above steps of comprehensive data preprocessing and modeling pipeline for a
classification task that includes data imputation, one-hot encoding for categorical variables,feature scaling, feature selection, and the choice of a Decision Tree Classifier as the predictive model. The pipeline ensures that data is processed consistently and efficiently before training and evaluating the model.


### Column Encoding And Features
These above steps of comprehensive data preprocessing and modeling pipeline for a
classification task that includes data imputation, one-hot encoding for categorical variables,feature scaling, feature selection, and the choice of a Decision Tree Classifier as the predictive model. The pipeline ensures that data is processed consistently and efficiently before training and evaluating the model.

Transformer and Scaling technics used here are : 
1.  SimpleImputer <br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Fills missing values with the most frequent value in the column. This is often used for categorical data.
2.  OneHotEncoder<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Creates binary columns for each unique value in categorical columns.
3.  MinMaxScaler<br>
          &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Scales the numerical features to a specified range, typically between 0 and 1.



Details about the features have been discussed here. '[Dataset](https://github.com/farhanshahriyar-cse/BitM_Browser-In-The-Middle-Phishing-Detection-using-Machine-Learning/tree/f984f930b06d1a10e8dd80116ba57002a6478381/Datasets)' folder.<br>


## Machine Learning Classifiers

SelectKBest with the chi-squared (chi2) scoring function is used for feature selection. It selects the top 6 best features based on their chi-squared statistics. This step reduces the dimensionality of the dataset, keeping the most informative features.

This dataset classifies as BitM phishing (1) or legitimate (0). The supervised machine learning models (classification) considered to train the BitM dataset are:

* Decision Tree
* Random Forest (RF)
* Naive Bayes (NB)
* Support Vector Machines (SVM)
* Multi-Layer Perceptron (MLP) 


All these models are trained on the dataset, and their performance is evaluated using the test dataset. 


The elaborate details of the attack of BitM Phishing and the models training are mentioned in [Phishing Detection in Browser-in-the-Middle: A Novel Empirical Approach Incorporating Machine Learning Algorithms](https://link.springer.com/chapter/10.1007/978-3-031-64067-4_9) *[![BitM Detection Book Chapter](https://img.shields.io/badge/Springer-BitM_Phishing_Detection_Book_Chapter-darkmagenta%09?style=flat-square&logo=semanticscholar&color=greenyellow)
](https://link.springer.com/chapter/10.1007/978-3-031-64067-4_9)*


## Results And Findings
Random Forest consistently shows the highest performance across metrics, with an accuracy of **0.99 (10 features) **and 0.94 (6 features), and the best F1 scores (0.99 and 0.96, respectively).

## Futurework

This project can be further expanded by developing a browser extension or creating a graphical user interface (GUI) or integrating on a IDS system that accepts a URL and determines whether it is legitimate or a BitM phishing attempt. 

