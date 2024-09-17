# From PCAP Network Traffic To Final CSV Dataset 




The process of preparing the final CSV file for analysis of the Browser-In-The-Middle (BITM) attack involves these key steps:

- Install Network Packet Analyzer: Begin by installing tshark, a tool used to analyze network packets, which helps capture live network traffic or read previously saved packets.

- Obtain .PCAP Files: Two .PCAP files are gathered using Wireshark—one representing safe browsing and the other for malicious BITM attacks.

- Load Data into Google Collaboratory: The .PCAP files are downloaded into Google Collaboratory from Google Drive using the !gdown command, providing a cloud environment for analysis.

- Convert .PCAP to CSV Format: To facilitate easier data manipulation, the .PCAP files are converted into CSV (Comma Separated Value) format using Pandas, a Python library for data analysis. This step involves adjusting display settings to view all columns and rows.

- Examine Data Frame: The Pandas library is used to determine the dimensions of the DataFrames, identify any missing values, and summarize the data, making the dataset easier to understand and work with.

- Analyze and Categorize Missing Values: Missing values in the data are detected using functions like .isnull() and .sum(). These values are then categorized and managed to ensure the integrity of the dataset.

- Label Data Frames: The CSV files are labeled to distinguish between normal and malicious data. Label 0 represents normal (safe) data, while Label 1 denotes malicious data.

- Concatenate Data: Finally, the two labeled CSV files (normal and malicious) are combined vertically to form a single, unified dataset. This consolidated DataFrame is saved as a new CSV file for further data preprocessing and analysis.

Finally, now we have our dataset BitM_Browser-In-The-Middle-Phishing-Detection_Dataset.csv.



## Columns or Features Introductory


1. frame.time_relative (float64): It represents the relative time at which each network
packet was captured. It's a floating-point number, which can help in analyzing the
temporal aspects of the network data.
2. frame.len (int64): This indicates the length of each network packet in bytes. It's an
integer column and can be important for understanding packet sizes and their impact
on network performance.
3. sll.pkttype (int64): This column represent the packet type as an integer. Packet types
can vary based on the networking technology used and can indicate whether a packet
is, for example, an Ethernet frame or something else.

4. sll.hatype (int64): Similar to the previous column, this one might represent the
hardware type (Link-layer address type) associated with the network packet, again
typically as an integer value.

5. ip.hdr_len (float64): This column represent the length of the IP header in bytes,
typically as a floating-point number. The IP header contains important information
about the IP packet.

6. ip.dsfield (object): This column appears to contain data related to the Differentiated
Services Field (DSField) in IP headers. DSField can be used for specifying Quality of
Service (QoS) and packet prioritization.

7. ip.dsfield.dscp (float64): This column represent the Differentiated Services Code
Point (DSCP) within the DSField. DSCP is used for QoS and packet classification.

8. ip.len (float64): This column likely represents the total length of the IP packet,
including both the header and payload, as a floating-point number.

9. ip.flags (object): This column could contain data related to IP flags. IP flags are used
to control various aspects of IP packet behavior, such as fragmentation.

10. ip.ttl (float64): This column might represent the Time to Live (TTL) field in the IP
header. TTL is used to limit the lifetime of a packet to prevent it from circulating
endlessly in the network.

11. ip.proto (float64): This column likely represents the protocol field in the IP header,
indicating the higher-level protocol (e.g., TCP, UDP) used in the packet.


These final features are used to preprocess and furthure training the machine learning models.

The elaborate details of the attack of BitM Phishing and the models training are mentioned in [Phishing Detection in Browser-in-the-Middle: A Novel Empirical Approach Incorporating Machine Learning Algorithms](https://link.springer.com/chapter/10.1007/978-3-031-64067-4_9) *[![BitM Detection Book Chapter](https://img.shields.io/badge/Springer-BitM_Phishing_Detection_Book_Chapter-darkmagenta%09?style=flat-square&logo=semanticscholar&color=greenyellow)
](https://link.springer.com/chapter/10.1007/978-3-031-64067-4_9)*
