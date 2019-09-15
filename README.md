# Bitcoin Service Check for Nagios/Icinga

Simple command-line utility to check status of a Bitcoin node

Uses Bitcoin protocol code from [@ayeowch/bitnodes](https://github.com/ayeowch/bitnodes) repo

## Setup

For clearnet testing, need Python2 + pip for python deps:
```
sudo apt-get install -y python-pip
sudo pip install -r requirements.txt
```

For *.onion node testing, also need:
```
sudo apt-get install -y tor
```

## Install check_bitcoin command
```
install -c -m 755 bitcoin-service-check.py /usr/lib/nagios/plugins/check_bitcoin
```

## Install check_bitcoin.conf in icinga2 configuration
```
cp check_bitcoin.conf /etc/icinga2/conf.d/
```

## Set bitcoinaddress (and optionally bitcoinport) in host object 
```
object Host "22tg6ufbwz6o3l2u.onion" {
    import "bitcoin-node"
    vars.bitcoinaddress = "22tg6ufbwz6o3l2u.onion"
}
```

## Manual Usage

./bitcoin-service-check.py [IP address or *.onion] [port]

Node is online:
```
% ./bitcoin-service-check.py jiuuuislm7ooesic.onion 8333
OK - 594893 /Satoshi:0.18.1/
```

Node is unreachable:
```
% ./bitcoin-service-check.py jiuuuislm7foobar.onion 8333
CRITICAL - Socket error: timed out: ('jiuuuislm7foobar.onion', 8333)
$ echo $?
2
```
