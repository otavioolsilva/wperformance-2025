Set of scripts to perform experiments over three different Python libraries capable of sniffing and processing packets from network interfaces: [Pyshark](https://github.com/KimiNewt/pyshark), [Scapy](https://scapy.net/) and [Pypcap](https://github.com/pynetwork/pypcap), which is used together with [dpkt](https://github.com/kbandla/dpkt). The scenarios of experiments considered are:

- TCP stream without bit rate limit for 10 seconds;
- UDP stream with bit rate limit[^1] for 10 seconds;
- UDP stream with bit rate limit of 2Mbits/s and defined number of blocks and their length[^2].

[^1]: Must be adjusted in the script `sniff-run.sh`.
[^2]: Also must be adjusted manually.

The metrics reported for consideration are: CPU usage, memory peak, number of packets processed and total running time.

These scripts were used in the paper "Performance Evaluation of Python Tools to Capture Packets in Resource-Constrained Devices", submited to the XXIV Workshop on Performance of Computing and Communication Systems ([WPerformance 2025](https://csbc.sbc.org.br/2025/wperformance/)), part of the 45º Brazilian Computer Society Congress ([CSBC 2025](https://csbc.sbc.org.br/2025/)), awaiting evaluation.

### Dependencies

All the experiments were conducted using Python 3.11.2 in the client side. The dependencies used and its versions were:

- For `sniff-dpkt.py`: [pypcap](https://pypi.org/project/pypcap/) (v1.3.0) and [dpkt](https://pypi.org/project/dpkt/) (v1.9.8) libraries.
- For `sniff-pyshark.py`: [Pyshark](https://pypi.org/project/pyshark/) (v0.6) library.
- For `sniff-scapy.py`: [Scapy](https://pypi.org/project/scapy/) (v2.6.0) library.
- For all the scripts: [psutil](https://pypi.org/project/psutil/) (v6.1.0) library.

To generate the simulation of a network stream of data, the application used was [iperf3](https://iperf.fr/) (v3.17.1).	

### How to execute

To run five iterations of an experiment, run the Bash script `sniff-run.sh` passing as arguments:

- Path of the Python interpreter;
- Path of the Python script;
- iperf3 server IP.

To define the experiment scenario, uncomment in this same script the one desired and adjust the parameters accordingly.

The Python scripts are configured to sniff the "eth0" interface for 50 seconds, these parameters can be changed in the code. Note that the Scapy and Pypcap + dpkt scripts must be executed with privileged permissions, while in the Pyshark one the user executing it must be on the "wireshark" group.