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

# Monitoring Bitcoin node with Icinga2

## Install check_bitcoin command
```
install -c -m 755 bitcoin-service-check.py /usr/lib/nagios/plugins/check_bitcoin
```

## Install check_bitcoin.conf in icinga2 configuration
```
cp check_bitcoin.conf /etc/icinga2/conf.d/
```

## Set bitcoinaddress and bitcoinport in icinga2 host definitions 
```
object Host "22tg6ufbwz6o3l2u.onion" {
  import "generic-host"

  // add the following 2 lines to host defintion:

  vars.bitcoinaddress = "22tg6ufbwz6o3l2u.onion"
  vars.bitcoinport = "8333"

}
```
