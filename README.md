# Mininet_Mesh-Topology_OSPF_BGP
A network emulator like Mininet allows one to simulate customized networks
in terms of a myriad of topologies in common knowledge as well as leaves room 
for flexible extension and experimentation. Its support for OpenFlow further
allows custom routing and extend combinations of such implementations for critical
network analysis. This project implements custom Mesh Topology in Mininet and records, visualizes and contrasts the critical differences in its performances when tested in conjunction with two well-known routing protocols: Border Gateway Protocol (BGP) and Open Shortest Path First Protocol (OSPF Protocol). We quantified our results in terms of 2 performance metrics: throughput and jitter. 

Getting Started
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

## Prerequisites
- Knowledge of Mininet
- Knowledge of Python API
- Ubuntu Command Line

## Installing
A step by step series of examples that tell you how to get a development env running
1. Install Mininet using the instructions in http://geekstuff.org/2018/09/26/mininet-tutorial/ 
  - Mininet VM download:  http://mininet.org/download/ 
  - https://github.com/mininet/mininet/wiki/Mininet-VM-Images 
(This can be just imported into VirtualBox or other VM program and should work as is.)

2. Do the Mininet walkthrough: http://mininet.org/walkthrough/ 

3. Go through the mininet tutorial examples (MIninet CLI andTopologies Part) in http://geekstuff.org/2018/09/26/mininet-tutorial/

### Background on wireshark:  
https://www.wireshark.org/docs/wsug_html_chunked/ChapterIntroduction.html 

### Python beginner’s guide 
https://wiki.python.org/moin/BeginnersGuide/Overview

## Running 
### Create the Topology
sudo -E python filename.py

### Generate TCP Flow and Throughput 
xterm display r1 r2 

For Client terminal, r1,

r1: iperf -c 10.1.12.2 -b 10Mb -p 6653

For Server terminal, r2,

r2: iperf -s -p 6653 -i 1 > filename.txt

cat filename.txt | grep sec | head -15 | tr - " " | awk '{print $4, $8}' > new_filename.txt
  
### Generate UDP Jitter
xterm display r1 r2 

For Client terminal, r1,

r1: iperf -c 10.1.12.2 -u -b 10Mb -p 5566 -t -15 

For Server terminal, r2,

r2: iperf -s -u -p 5566 -i 1 > filename.txt

cat filename.txt | grep sec | head -15 | tr - " " | awk '{print $4, $10}' > new_filename.txt

### Generate Graph Plots

(Same for both TCP Throughput and UDP Jitter. Shown for UDP Jitter) 

r2: gnuplot

gnuplot>plot "new_filename_tcp.txt" 

title"Throughput" with linespoint

"new_filename_udp.txt" title "Jitter UDP" with linespoint

## Built With
Oracle Virtual Box(v6.0,22) - Virtualization Software 
Mininet - Network Simulator 
Ubuntu(v20.04.1) - Operating System

## Author
Vriddhi Pai
