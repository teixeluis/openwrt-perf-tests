# MT7620A vs QCA9533-AL3A performance tests:

## Overview

List of performance tests executed against a reference device, the TP-Link TL-WR841N, 
and the Youku YK L1. The first has an Atheros QCA9533-AL3A chipset, while the later
is based on the Ralink/MediaTek MT7620A. The goal is to understand the performance
of the Youku compared to the reference device which is known to peform according to
its hardware specifications using OpenWrt.

## Description of the setup

For performing the tests, a main router was used as AP or STA depending on the test. 
The particular unit was a UniElec U7621-06 featuring a MediaTek MT7621 chip and 
two PCIe wifi cards installed - a MT7603E and a MT7612E. This router was running 
OpenWrt 19.07.5 and one of the wifi cards was dedicated to the performance tests.

A regular PC running Ubuntu linux was attached to one of its 1 Gbps Ethernet ports, 
and was used for running the iperf3 client instance.

The main router and the two routers under test where separated by approximately 3
meters, in a triangular pattern.

![alt text](https://raw.githubusercontent.com/teixeluis/openwrt-perf-tests/main/openwrt-perf-tests-setup.png "Tests setup")

The TP-Link router was running OpenWRT release 15.05.1, whereas the Youku was running
a OpenWRT snapshot build (r15345-077c16fa05) manually compiled from the following 
separate branch:

https://git.openwrt.org/openwrt/staging/dangole.git

## Tests

Tests were executed by running the iperf3 tool in the two test routers and in the Ubuntu
PC. The routers had iperf3 running as server (iperf -s), whereas the PC had iperf3 running
as client with traffic set to flow in either forward or reverse direction depending on
the test.

1. Main Router is WDS AP, Youku and tplink are WDS STA

1.1. HT20:

### tplink:

**Reverse direction (iperf3 -R -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  49.1 MBytes  41.2 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  49.0 MBytes  41.1 Mbits/sec                  receiver


Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  44.1 MBytes  37.0 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  43.9 MBytes  36.8 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  52.2 MBytes  43.8 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  51.7 MBytes  43.4 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  47.6 MBytes  40.0 Mbits/sec    1             sender
[  5]   0.00-10.00  sec  47.1 MBytes  39.5 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  50.1 MBytes  42.0 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  50.0 MBytes  41.9 Mbits/sec                  receiver
```

**Forward direction (iperf3 -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  71.1 MBytes  59.6 Mbits/sec    1             sender
[  5]   0.00-10.00  sec  70.6 MBytes  59.2 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  65.4 MBytes  54.9 Mbits/sec    5             sender
[  5]   0.00-10.00  sec  65.0 MBytes  54.5 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  73.9 MBytes  62.0 Mbits/sec    1             sender
[  5]   0.00-10.00  sec  73.4 MBytes  61.6 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  69.3 MBytes  58.2 Mbits/sec    3             sender
[  5]   0.00-10.00  sec  68.7 MBytes  57.7 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  67.9 MBytes  57.0 Mbits/sec   26             sender
[  5]   0.00-10.00  sec  67.3 MBytes  56.5 Mbits/sec                  receiver
```


### Youku:

**Reverse direction (iperf3 -R -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.15  sec  26.2 MBytes  21.7 Mbits/sec   40             sender
[  5]   0.00-10.00  sec  25.6 MBytes  21.5 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.12  sec  26.1 MBytes  21.6 Mbits/sec   24             sender
[  5]   0.00-10.00  sec  25.4 MBytes  21.3 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.05  sec  27.0 MBytes  22.5 Mbits/sec    9             sender
[  5]   0.00-10.00  sec  26.2 MBytes  21.9 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.01  sec  22.1 MBytes  18.5 Mbits/sec   33             sender
[  5]   0.00-10.00  sec  21.7 MBytes  18.2 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.01  sec  23.9 MBytes  20.0 Mbits/sec   61             sender
[  5]   0.00-10.00  sec  23.2 MBytes  19.5 Mbits/sec                  receiver
```

**Forward direction (iperf3 -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  23.3 MBytes  19.5 Mbits/sec   25             sender
[  5]   0.00-10.00  sec  22.5 MBytes  18.9 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  20.1 MBytes  16.9 Mbits/sec   18             sender
[  5]   0.00-10.00  sec  19.0 MBytes  15.9 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  22.7 MBytes  19.0 Mbits/sec    8             sender
[  5]   0.00-10.00  sec  21.9 MBytes  18.4 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  23.7 MBytes  19.9 Mbits/sec   13             sender
[  5]   0.00-10.00  sec  22.7 MBytes  19.0 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  22.6 MBytes  18.9 Mbits/sec   14             sender
[  5]   0.00-10.11  sec  21.7 MBytes  18.0 Mbits/sec                  receiver
```

1.2. HT40 forced:

### tplink:


**Reverse direction (iperf3 -R -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  47.8 MBytes  40.1 Mbits/sec    6             sender
[  5]   0.00-10.00  sec  47.7 MBytes  40.0 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  52.1 MBytes  43.7 Mbits/sec    1             sender
[  5]   0.00-10.00  sec  51.4 MBytes  43.2 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  51.0 MBytes  42.8 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  51.0 MBytes  42.8 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  52.0 MBytes  43.6 Mbits/sec    1             sender
[  5]   0.00-10.00  sec  51.5 MBytes  43.2 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  50.4 MBytes  42.3 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  49.8 MBytes  41.8 Mbits/sec                  receiver
```

**Forward direction (iperf3 -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  98.1 MBytes  82.3 Mbits/sec   64             sender
[  5]   0.00-10.00  sec  97.7 MBytes  81.9 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  97.8 MBytes  82.0 Mbits/sec   27             sender
[  5]   0.00-10.00  sec  97.3 MBytes  81.7 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  97.7 MBytes  81.9 Mbits/sec   58             sender
[  5]   0.00-10.00  sec  97.3 MBytes  81.6 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec   101 MBytes  85.0 Mbits/sec   61             sender
[  5]   0.00-10.00  sec   101 MBytes  84.4 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec   100 MBytes  83.9 Mbits/sec   45             sender
[  5]   0.00-10.00  sec  99.7 MBytes  83.6 Mbits/sec                  receiver
```

### Youku:

**Reverse direction (iperf3 -R -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.01  sec  62.8 MBytes  52.6 Mbits/sec   18             sender
[  5]   0.00-10.00  sec  62.3 MBytes  52.2 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.03  sec  73.9 MBytes  61.8 Mbits/sec    6             sender
[  5]   0.00-10.00  sec  72.9 MBytes  61.2 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.02  sec  62.8 MBytes  52.6 Mbits/sec    9             sender
[  5]   0.00-10.00  sec  61.9 MBytes  51.9 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.01  sec  69.0 MBytes  57.9 Mbits/sec   11             sender
[  5]   0.00-10.00  sec  68.4 MBytes  57.4 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.01  sec  65.7 MBytes  55.1 Mbits/sec   12             sender
[  5]   0.00-10.00  sec  65.0 MBytes  54.5 Mbits/sec                  receiver
```

**Forward direction (iperf3 -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  83.6 MBytes  70.1 Mbits/sec    4             sender
[  5]   0.00-10.03  sec  81.1 MBytes  67.8 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  81.6 MBytes  68.4 Mbits/sec   70             sender
[  5]   0.00-10.01  sec  80.5 MBytes  67.4 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  94.1 MBytes  78.9 Mbits/sec    8             sender
[  5]   0.00-10.06  sec  91.5 MBytes  76.3 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  99.2 MBytes  83.2 Mbits/sec   81             sender
[  5]   0.00-10.02  sec  97.3 MBytes  81.4 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  85.9 MBytes  72.0 Mbits/sec    8             sender
[  5]   0.00-10.03  sec  84.8 MBytes  70.9 Mbits/sec                  receiver
```

2. Main Router is WDS STA, Youku and tplink are WDS AP


2.1. HT20:

### tplink:

**Reverse direction (iperf3 -R -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  48.2 MBytes  40.5 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  48.2 MBytes  40.5 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  51.3 MBytes  43.0 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  50.2 MBytes  42.1 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  49.3 MBytes  41.4 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  48.4 MBytes  40.6 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  51.4 MBytes  43.1 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  50.9 MBytes  42.7 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  50.0 MBytes  42.0 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  49.4 MBytes  41.4 Mbits/sec                  receiver
```

**Forward direction (iperf3 -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  97.2 MBytes  81.5 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  96.8 MBytes  81.2 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  88.6 MBytes  74.3 Mbits/sec    1             sender
[  5]   0.00-10.00  sec  88.2 MBytes  74.0 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  93.7 MBytes  78.6 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  93.3 MBytes  78.3 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  88.3 MBytes  74.1 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  87.8 MBytes  73.6 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  84.4 MBytes  70.8 Mbits/sec    1             sender
[  5]   0.00-10.00  sec  83.9 MBytes  70.4 Mbits/sec                  receiver
```


### Youku:

**Reverse direction (iperf3 -R -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  20.0 MBytes  16.8 Mbits/sec  161             sender
[  5]   0.00-10.00  sec  19.3 MBytes  16.1 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  17.2 MBytes  14.4 Mbits/sec  106             sender
[  5]   0.00-10.00  sec  16.8 MBytes  14.1 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.01  sec  30.7 MBytes  25.8 Mbits/sec   17             sender
[  5]   0.00-10.00  sec  30.2 MBytes  25.3 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.04  sec  24.4 MBytes  20.4 Mbits/sec   55             sender
[  5]   0.00-10.00  sec  24.1 MBytes  20.2 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.02  sec  12.5 MBytes  10.4 Mbits/sec   88             sender
[  5]   0.00-10.00  sec  12.3 MBytes  10.3 Mbits/sec                  receiver
```

**Forward direction (iperf3 -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  18.0 MBytes  15.1 Mbits/sec   21             sender
[  5]   0.00-10.02  sec  17.3 MBytes  14.5 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  13.9 MBytes  11.6 Mbits/sec   11             sender
[  5]   0.00-10.10  sec  13.2 MBytes  11.0 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  19.2 MBytes  16.1 Mbits/sec   30             sender
[  5]   0.00-10.00  sec  18.5 MBytes  15.5 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  18.3 MBytes  15.3 Mbits/sec   13             sender
[  5]   0.00-10.00  sec  17.8 MBytes  14.9 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  17.3 MBytes  14.5 Mbits/sec   13             sender
[  5]   0.00-10.03  sec  16.3 MBytes  13.7 Mbits/sec                  receiver
```

2.2. HT40 forced:

### tplink:

**Reverse direction (iperf3 -R -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  46.1 MBytes  38.7 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  45.5 MBytes  38.1 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  44.4 MBytes  37.2 Mbits/sec    2             sender
[  5]   0.00-10.00  sec  44.0 MBytes  36.9 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  46.1 MBytes  38.7 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  46.1 MBytes  38.6 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  46.8 MBytes  39.3 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  46.4 MBytes  38.9 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  45.9 MBytes  38.5 Mbits/sec    0             sender
[  5]   0.00-10.00  sec  45.8 MBytes  38.4 Mbits/sec                  receiver
```

**Forward direction (iperf3 -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec   103 MBytes  86.4 Mbits/sec   41             sender
[  5]   0.00-10.00  sec   102 MBytes  85.9 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  97.2 MBytes  81.6 Mbits/sec   19             sender
[  5]   0.00-10.00  sec  96.6 MBytes  81.0 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec   105 MBytes  87.8 Mbits/sec   50             sender
[  5]   0.00-10.00  sec   104 MBytes  87.6 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec   103 MBytes  86.6 Mbits/sec   24             sender
[  5]   0.00-10.00  sec   103 MBytes  86.0 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec   101 MBytes  84.6 Mbits/sec   23             sender
[  5]   0.00-10.00  sec   100 MBytes  84.1 Mbits/sec                  receiver
```

### Youku:

**Reverse direction (iperf3 -R -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.03  sec  95.4 MBytes  79.8 Mbits/sec  106             sender
[  5]   0.00-10.00  sec  95.0 MBytes  79.7 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.06  sec  66.2 MBytes  55.3 Mbits/sec   45             sender
[  5]   0.00-10.00  sec  65.7 MBytes  55.1 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.07  sec  83.1 MBytes  69.2 Mbits/sec   90             sender
[  5]   0.00-10.00  sec  82.5 MBytes  69.2 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.02  sec  88.1 MBytes  73.8 Mbits/sec   46             sender
[  5]   0.00-10.00  sec  87.2 MBytes  73.2 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.04  sec  89.1 MBytes  74.4 Mbits/sec   47             sender
[  5]   0.00-10.00  sec  88.0 MBytes  73.8 Mbits/sec                  receiver
```

**Forward direction (iperf3 -c ...)**

```
Test 1:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  82.8 MBytes  69.4 Mbits/sec   29             sender
[  5]   0.00-10.06  sec  81.2 MBytes  67.7 Mbits/sec                  receiver

Test 2:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  87.3 MBytes  73.2 Mbits/sec   11             sender
[  5]   0.00-10.01  sec  85.3 MBytes  71.4 Mbits/sec                  receiver

Test 3:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec  96.8 MBytes  81.2 Mbits/sec   21             sender
[  5]   0.00-10.01  sec  95.0 MBytes  79.6 Mbits/sec                  receiver

Test 4:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec   114 MBytes  95.9 Mbits/sec    1             sender
[  5]   0.00-10.01  sec   112 MBytes  93.9 Mbits/sec                  receiver

Test 5:

[ ID] Interval           Transfer     Bitrate         Retr
[  5]   0.00-10.00  sec   105 MBytes  87.7 Mbits/sec    4             sender
[  5]   0.00-10.03  sec   102 MBytes  85.6 Mbits/sec                  receiver
```
