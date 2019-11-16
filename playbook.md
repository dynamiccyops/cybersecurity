# Find Name Servers
host -t ns megacorpone.com

# Find Mail Servers
host -t mx megacorpone.com

# Find Web Servers
host www.megacorpone.com

# Find Nonexists
host idontexist.megacorpone.com

# Create List for Brute Force Script
echo www > list.txt
echo ftp >> list.txt
echo mail >> list.txt
echo owa >> list.txt
echo proxy >> list.txt
echo router >> list.txt
for ip in $(cat list.txt);do host $ip.megacorpone.com;done

# Reverse Lookup Brute Force
for ip in $(seq 155 190);do host 50.7.67.$ip;done |grep -v "not found"

# DNS Zone Transfer
host -l <domain name> <dns server address>

host -l megacorpone.com ns1.megacorpone.com
host -l megacorpone.com ns2.megacorpone.com

# Cleaner Format
host -t ns megacorpone.com | cut -d " " -f 4

#!/bin/bash
# Simple Zone Transfer Bash Script
# $1 is the first argument given after the bash script
# Check if argument was given, if not, print usage
if [ -z "$1" ]; then
echo "[*] Simple Zone transfer script"
echo "[*] Usage
: $0 <domain name> "
exit 0
fi
# if argument was given, identify the DNS servers for the domain
for server in $(host -t ns $1 |cut -d" " -f4);do
# For each of these servers, attempt a zone transfer
host -l $1 $server |grep "has address"
done

# Save Script and Run It
chmod 755 dns-axfr.sh
./dns-axfr.sh megacorpone.com

dnsrecon -d megacorpone.com -t axfr

dnsenum zonetransfer.me

# CONNECT scanning
nc -nvv -w 1 -z 10.0.0.19 3388-3390

# UDP Scanning
nc -nv -u -z -w 1 10.0.0.19 160-162

## CROSSING THE LINE WITH NMAP

# Wrap the following in a script:

iptables -I INPUT 1 -s 10.0.0.19 -j ACCEPT
iptables -I OUTPUT 1 -d 10.0.0.19 -j ACCEPT

iptables -Z
nmap -sT 10.0.0.19

# 1 IP 65K Ports
# ~3MB of Traffic

# ~254 Class C Range
# ~1000MB