# Network Attack Detection using Machine Learning

## Description

This project leverages machine learning techniques to classify network attacks such as Port Scanning, Denial of Service (DoS), and malware. The input data is in the Netflow V9 format, which is a standard format used by Cisco.

The classification is performed using the following models:

- K-Nearest Neighbors (KNN)
- Support Vector Machine Classifier (SVC) with RBF (Radial Basis Function) kernel
- Pipeline with Principal Component Analysis (PCA) and Support Vector Machine Classifier (SVC)
- Bagging Classifier (based on SVC with RBF kernel)
- Random Forest Classifier
- Extra Trees Classifier
- Neural Network (MLPClassifier)

The project is implemented in Python using Jupyter Notebook and several popular libraries, including [UMAP](https://umap-learn.readthedocs.io/), [Pandas](https://pandas.pydata.org), [NumPy](https://numpy.org), [Scikit-Learn](https://scikit-learn.org/), [Matplotlib](https://matplotlib.org), and [Seaborn](https://seaborn.pydata.org).

## Notebook

The notebook is accessible [here](./src/network-attack-detection.ipynb) for direct viewing on GitHub. Alternatively, you can use NbViewer to access the notebook via [this link](https://nbviewer.org/github/lucadibello/network-attack-detection/blob/main/src/network-attack-detection.ipynb).

## Presentation

The Keynote presentation in PDF format is accessible [here](./doc/presentation.pdf).

## Datasets

The dataset used for this project is in the NetFlow V9 format (documented by Cisco, available [here](https://www.cisco.com/en/US/technologies/tk648/tk362/technologies_white_paper09186a00800a3db9.html)). It consists of two files: train_net.csv and test_net.csv.

The train_net.csv file provides information on when a particular alert is likely to occur, while the test_net.csv file is used solely for testing purposes and does not contain a target variable for evaluating model performance.

The dataset is quite large:

- `train_net.csv`: approximately 4 million packets (from 14'066 unique network hosts)
- `test_net.csv`: approximately 2 million packets (from 6'186 unique network hosts)

### Dataset features

* **FLOW_ID**: A unique identifier for the flow
* **PROTOCOL_MAP**: A string representing the protocol used in the flow, possible values include "ICMP", "TCP", "UDP", "IGMP", "GRE", "ESP", "AH", "EIGRP", "OSPF", "PIM", "IPV6-ICMP", "IPV6-IP", "IPV6-ROUTE", "IPV6-FRAG", "IPV6-NONXT", "IPV6-OPTS", and others.
* **L4_SRC_PORT**: The source port number in the flow, possible values range from 0 to 65535.
* **IPV4_SRC_ADDR**: The source IPv4 address in the flow, represented as a string in dotted decimal notation (e.g., "192.168.0.1").
* **L4_DST_PORT**: The destination port number in the flow, possible values range from 0 to 65535.
* **IPV4_DST_ADDR**: The destination IPv4 address in the flow, represented as a string in dotted decimal notation (e.g., "192.168.0.2").
* **FIRST_SWITCHED**: The time at which the flow started, measured in seconds since the epoch (January 1, 1970).
* **FLOW_DURATION_MILLISECONDS**: The duration of the flow in milliseconds.
* **LAST_SWITCHED**: The time at which the flow ended, measured in seconds since the epoch (January 1, 1970).
* **PROTOCOL**: The protocol used in the flow, possible values include 1 (ICMP), 6 (TCP), 17 (UDP), and others.
* **TCP_FLAGS**: The TCP flags set in the flow, represented as a binary string (e.g., "100101").
* **TCP_WIN_MAX_IN**: The maximum advertised window size (in bytes) for incoming traffic.
* **TCP_WIN_MAX_OUT**: The maximum advertised window size (in bytes) for outgoing traffic.
* **TCP_WIN_MIN_IN**: The minimum advertised window size (in bytes) for incoming traffic.
* **TCP_WIN_MIN_OUT**: The minimum advertised window size (in bytes) for outgoing traffic.
* **TCP_WIN_MSS_IN**: The maximum segment size (in bytes) for incoming traffic.
* **TCP_WIN_SCALE_IN**: The window scale factor for incoming traffic.
* **TCP_WIN_SCALE_OUT**: The window scale factor for outgoing traffic.
* **SRC_TOS**: The Type of Service (ToS) value for the source IP address.
* **DST_TOS**: The Type of Service (ToS) value for the destination IP address.
* **TOTAL_FLOWS_EXP**: The total number of expected flows.
* **MIN_IP_PKT_LEN**: The minimum length (in bytes) of IP packets in the flow.
* **MAX_IP_PKT_LEN**: The maximum length (in bytes) of IP packets in the flow.
* **TOTAL_PKTS_EXP**: The total number of expected packets in the flow.
* **TOTAL_BYTES_EXP**: The total number of expected bytes in the flow.
* **IN_BYTES**: The number of bytes received in the flow.
* **IN_PKTS**: The number of packets received in the flow.
* **OUT_BYTES**: The number of bytes sent in the flow.
* **OUT_PKTS**: The number of packets sent in the flow.
* **ANALYSIS_TIMESTAMP**: The time at which the flow was analyzed, measured in seconds since the epoch (January 1, 1970).
* **ANOMALY**: A binary flag indicating whether the flow contains an anomaly (1 = true, 0 = false).
* **ALERT**: (<u>only available in training set</u>) The kind of attack that has been detected on the current flow. This are the possible values:
  - **None**: No attack has been detected
  - **Port scanning**: The flow is a port scanning attack 
  - **Denial of Service**: The flow is a DoS attack
  - **Malware**: The flow is a malware attack
* **ID**: A unique identifier for the flow.

### Dataset authors

Maria-Elena Mihailescu, Darius Mihai, Mihai Carabas, Mikolaj Komisarek, Marek Pawlicki, Witold Holubowicz, Rafal Kozik:
The Proposition and Evaluation of the RoEduNet-SIMARGL2021 Network Intrusion Detection Dataset. Sensors 21(13): 4319 (2021)

[Kaggle link](https://www.kaggle.com/datasets/ashtcoder/network-data-schema-in-the-netflow-v9-format)
