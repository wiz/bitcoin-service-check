# Bitcoin Service Check

Simple command-line utility to check status of a Bitcoin node
Based on code from @ayeowch/bitnodes project

## Setup

Basic node testing
```bash
apt-get install -y python-pip
pip install -r requirements.txt
./bitcoin-service-check.py 1.2.3.4 8333
```

Additionally, for *.onion node testing:
```bash
apt-get install -y tor
./bitcoin-service-check.py foo.onion 8333
```
