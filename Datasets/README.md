# From PCAP Network Traffic To Final CSV Dataset 


The process of preparing the final CSV file for analysis of the Browser-In-The-Middle (BITM) attack involves these key steps:

Install Network Packet Analyzer: Begin by installing tshark, a tool used to analyze network packets, which helps capture live network traffic or read previously saved packets.

Obtain .PCAP Files: Two .PCAP files are gathered using Wireshark—one representing safe browsing and the other for malicious BITM attacks.

Load Data into Google Collaboratory: The .PCAP files are downloaded into Google Collaboratory from Google Drive using the !gdown command, providing a cloud environment for analysis.

Convert .PCAP to CSV Format: To facilitate easier data manipulation, the .PCAP files are converted into CSV (Comma Separated Value) format using Pandas, a Python library for data analysis. This step involves adjusting display settings to view all columns and rows.

Examine Data Frame: The Pandas library is used to determine the dimensions of the DataFrames, identify any missing values, and summarize the data, making the dataset easier to understand and work with.

Analyze and Categorize Missing Values: Missing values in the data are detected using functions like .isnull() and .sum(). These values are then categorized and managed to ensure the integrity of the dataset.

Label Data Frames: The CSV files are labeled to distinguish between normal and malicious data. Label 0 represents normal (safe) data, while Label 1 denotes malicious data.

Concatenate Data: Finally, the two labeled CSV files (normal and malicious) are combined vertically to form a single, unified dataset. This consolidated DataFrame is saved as a new CSV file for further data preprocessing and analysis.

Finally, now we have our dataset BitM_Browser-In-The-Middle-Phishing-Detection_Dataset.
