
# Installation Instructions

This project requires Python 3 and several external libraries. Below are the instructions to set up the project environment and install the necessary dependencies.

## Prerequisites

Ensure that you have Python 3 installed on your system. You can download it from [python.org](https://www.python.org/downloads/).

# For ALL C PROGRAMS 
Change the Network device to the device that you want to monitor 

# Packet Capture and Analysis Tool

This tool is designed to capture and analyze network packets, focusing on connections and their characteristics. It tracks network traffic, identifying unique connections based on source and destination IP addresses and ports. For each connection, it captures a configurable number of packets and organizes them into pcap files. This is particularly useful for network monitoring, traffic analysis, and forensic investigations.

## Compilation

Before running the program, you need to compile it using GCC. Make sure you have `libpcap` installed on your system as the program depends on it for packet capturing.

To compile the program, run the following command:

```bash
gcc -o samp sampling.c -lpcap
```

## Running the Program

After compiling, you can run the program with the following command:

```bash
./samp <PacketsPerFile> <PacketsPerConnection> <DurationInSeconds>
```

Replace `<PacketsPerFile>`, `<PacketsPerConnection>`, and `<DurationInSeconds>` with your desired values.

## Prerequisites

Ensure `libpcap` is installed on your system. If it's not installed, you can typically install it via your package manager. For example, on Debian-based systems, you can use:

```bash
sudo apt-get install libpcap-dev
```

# Evaluation Program

The Evaluation Program is designed for focused packet analysis between specific source and destination IP addresses. It captures packets matching the provided IP addresses and saves them for further analysis. This functionality is crucial for targeted network traffic analysis, especially in scenarios requiring detailed examination of communication between particular network nodes.

## Compilation

Similar to the Packet Capture and Analysis Tool, this program also requires the `libpcap` library. Ensure that it is installed on your system.

To compile the Evaluation Program, use the following command:

```bash
gcc -o eval evaluation.c -lpcap
```

## Running the Program

After compiling, the program can be executed with:

```bash
./eval <SrcIP> <DstIP>
```

Replace `<SrcIP>` and `<DstIP>` with the source and destination IP addresses you want to analyze.

# Track Program

The Track Program is tailored for capturing network packets related to a specific IP address. It focuses on either the source or the destination IP matching the provided IP, making it an efficient tool for targeted network analysis. This feature is particularly valuable for tracking the activities of a specific network node or for focused network troubleshooting.

## Compilation

The Track Program also requires the `libpcap` library. Before running the program, it needs to be compiled with GCC.

To compile the Track Program, execute the following command:

```bash
gcc -o track track.c -lpcap
```

## Running the Program

Once compiled, you can run the program as follows:

```bash
./track <IP>
```

Replace `<IP>` with the IP address you wish to track.

Please ensure `libpcap` is installed on your system. If it is not, you can install it using your system's package manager.

# Python PCAP Analysis Tool

Fr this program on line 52 (local_network = ipaddress.ip_network('192.168.1.0/24', strict=False)) chnage the network rnage 192.168.1.0/24 to your network range to make it work. This Python program is designed to analyze PCAP files, specifically identifying miner and warning connections based on certain criteria. It reads network packets from PCAP files, checks for specific patterns indicative of mining activity, and logs external IP connections for further investigation. The tool is ideal for network administrators and cybersecurity analysts to monitor and analyze network traffic efficiently.

## Dependencies

The program requires the following Python packages:
- scapy
- ipaddress (included in Python Standard Library)

## Installing Dependencies

You can install the required external library using `pip`. Run the following command in your terminal:

```bash
pip install scapy
```

## Running the Program

To run the program, navigate to the directory containing the script and execute it with Python:

```bash
python pcap_analysis_tool.py <folder_path>
```

Replace `<folder_path>` with the path to the folder containing your PCAP files. The program will analyze the files and output the results to specified log files.


## Installing Dependencies

Install the required external libraries using `pip`. Run the following command in your terminal:

```bash
pip install Flask requests scapy matplotlib Pillow
```


## Running the Application

After installing the dependencies, you can run your Flask application. Make sure you are in the directory containing your `server.py` and on server.py on line 223 chnage the network range from 192.168.1.0/24 to your network range to make this work (or your main Python script for the Flask app) and run:

```bash
python server.py
```



The application should now be running and accessible in your web browser.


## Project Description

This dashboard is intended to be used to monitor the network and detect miners and possible miners. It has been tested with Cudo Miner.

It consists on 5 steps:
    - Sampling
    - Sampling analyze
    - Track
    - Monitoring data
    - Analyzer configuration

## Sampling 

In this page you are able to slect parameters for sampling your network. You can select how many packets per unique connection you capture, how many packets per file or how much time listening to the network. The intention is to detect any new miner connected after the systems starts sampling. We understand as unique connection as the elements src ip, src port, dst ip and dst port. We use libcap lib in C to perform the packet collection.

## Analise Sampling 

After a sampling session, all the data is stored on a folder (date of the sampling). On this step it will detect from all the files in the folder, possible miners (warnings) and miners. 

## Track

After analyzing the samples, the connections are displayed in 3 categories, mining connections, warning connections and machines. Each one will allow to start a new collector focused on that specific machine. The objective is to gather enough data for plotting or to detect a miner from a warning connection. If we monitor a warning, we would go back to analise sampling to check again if we can find traces of a miner.

## Monitoring Data

Here we can plot data after tracking a mining connection. We mainly estimate just from network packets the hash rate, bandwidth and power consumption.
Bandwidth can be easily calculated from the packets collected.
The innovation of this project are the calculation of the hash rate and the power consumption. We have used HWiNFO to obtain statistics of power consumption on real time and cudo miner launcher for hash estimation metrics. With he help of those applications we are able to calculate with certain conditions, the hash rate from the nonces sent from the client app to the mining pool. If we are using this specific miner and only mining one coin simultaneously, and a coint that mines using cpu power. We are able to roughly estimate the hash rate.
Once we have estimated the hashrate considering benchmark performance of cpu's we are able to calculate the power consumption.

## Analyzer configuration

This page allows to block and unblock ips. If we find a suspicious connection that we want to block it can be done with 2 simple clicks. On the moment of ban, it will also show some information about the ip to ban so we can know what we are blocking. It keeps track of the blocked connections, in case we block an essential service for our company. Therefore in the same way we block, we can unblock them, also showing some information.