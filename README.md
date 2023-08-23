# Simple IP sweeper

IP Sweeper is a command-line tool for scanning and monitoring a range of IP addresses. It's designed to help network administrators and security professionals discover active devices on a network.

## About

IP Sweeper is a powerful utility for network discovery and monitoring. 
Whether you're managing a small home network or a large corporate infrastructure, IP Sweeper simplifies the process of identifying active devices and their status.

## Installation and Usage
Simply clone the repo and execute the file as shown below:

```
# Example installation steps
git clone https://github.com/Het-Joshi/ip-sweeper.git
cd ip-sweeper
chmod +x ipsweep.sh 
./ipsweep <enter first 3 ranges eg. 192.163.1>
```

## Code Breakdown

```bash

for ip in `seq 1 245 `;do
```
This line starts a for loop. It iterates through a sequence of numbers from 1 to 245 using the seq command. The numbers represent the last octet of IP addresses.

```bash

ping -c 1 $1.$ip|grep "64 bytes"|cut -d "" -f 4|tr -d ";"&
```
This is the core of the script where it performs the following operations for each IP address in the specified range:


- **ping -c 1 $1.$ip**: This line sends a single ICMP echo request packet to the IP address formed by concatenating the value of $1 (the first argument passed to the script) with the current value of $ip. This checks if the IP address is reachable.

- **|**: This pipe character is used to pass the output of the ping command to the next command.

- **grep "64 bytes"**: This command searches for lines in the ping command output that contain the text "64 bytes." This is typically found in a successful ping response.

- **cut -d " " -f 4**: It takes the output of grep and splits it into fields using space as the delimiter. It then extracts the fourth field, which is the IP address itself.

- **tr -d ";"** : This command removes any semicolons from the IP address (though there shouldn't be any semicolons in a standard ping response).

- **&**: The ampersand at the end of the line runs each ping command in the background, allowing multiple pings to occur simultaneously. This can speed up the process when pinging a range of IP addresses.

The loop continues until it has checked all the IP addresses from 1 to 245 in the range specified.

Please note that this script assumes the first argument passed to the script ($1) is the base IP address (e.g., 192.161.1), and it appends the last octet to scan a range of IP addresses in that subnet. Additionally, it's set up to extract IP addresses from the output of the ping command, which may vary depending on the system and its configuration.
