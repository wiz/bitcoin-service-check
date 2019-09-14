# Bitcoin Service Check

Simple command-line utility to check status of a Bitcoin node

Uses Bitcoin protocol code from [@ayeowch/bitnodes](https://github.com/ayeowch/bitnodes) repo

## Setup

For clearnet testing, need Python2 + pip:
```
apt-get install -y python-pip
```

For *.onion node testing, also need:
```
apt-get install -y tor
```

Install deps using pip:
```
pip install -r requirements.txt
```

## Usage

./bitcoin-service-check.py [IP address or *.onion] [port]

Node is online:
```
% ./bitcoin-service-check.py jiuuuislm7ooesic.onion 8333
594893
/Satoshi:0.18.1/
```

Node is unreachable:
```
% ./bitcoin-service-check.py jiuuuislm7foobar.onion 8333
Socket error: timed out: ('jiuuuislm7foobar.onion', 8333)
$ echo $?
1
```
