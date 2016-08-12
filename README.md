# TorBalancer

Balance traffic between multiple Tor clients.

Keeps the circuit and returns connections according to onion address.

```
HAProxy <--HTTP-->  DeleGate1 <--socks--> Tor1  <-->  Rendezvous Points
                    DeleGate2 <--socks--> Tor2  <-->  Rendezvous Points
                    ...
                    DeleGate9 <--socks--> Tor9  <-->  Rendezvous Points
```

Or with Polipo instead of Delegate:

```
HAProxy <--HTTP-->  Polipo1 <--socks--> Tor1  <-->  Rendezvous Points
                    Polipo2 <--socks--> Tor2  <-->  Rendezvous Points
                    ...
                    Polipo9 <--socks--> Tor9  <-->  Rendezvous Points
```

![Stats GUI](https://github.com/ahmia/TorBalancer/blob/master/stats.png)


## Setup TorBalancer

- Installer script will install HAProxy, DeleGate or Polipo and Tor
- You can install manually Tor in Tor2web mode
- You can manually setup fast Tor2webRendezvousPoints

Tor2web mode and Tor2webRendezvousPoints selection is optional.

If you want to use Tor to access public WWW sites then do not use Tor2web mode. Tor2web mode only allows connections to onion addresses.

## You can select Polipo or Delegate version of the proxy.

```sh
cd polipo-version
cd delegate-version
```

```sh
sudo ./install.sh
```

## Start the system

```sh
$ bash opentors.sh
```

## Finally, you can test your HAProxy:

```sh
$ curl -x localhost:3128 http://msydqstlz2kzerdg.onion/
$ http://localhost:5000/stats
```

## Shutdown

You can kill your Tors, DeleGates or Polipo and HAProxy by

```sh
$ killall haproxy
$ killall tor
$ kill $(ps aux | grep 'delegate' | awk '{print $2}')
$ kill $(ps aux | grep 'polipo' | awk '{print $2}')
```
