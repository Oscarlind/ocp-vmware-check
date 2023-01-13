# ocp-vmware-check
This script is simply fetching information about the VM's that are running in VMware for the OCP clusters. It creates a table of information about them when requested.

## Pre-requirements
This is created using python 3.8.

Install the required modules by running `python -m pip install -r requirements.txt`
Populate the `user` and `pwd` fields on line 19 and 20 to make it possible to establish a connection to vCenter.
Also change the path with the aliases for the different clusters in the dictionary, starting on line: 28

> TIP: Copy the script to a place in your path - then you can run it by just typing `vmcheck` globally from the machine.

```
mkdir /opt/vmcheck
cp vmcheck /opt/vmcheck

echo 'export PATH="/opt/vmcheck:$PATH"' >> ~/.bashrc

source ~/.bashrc
```

## How to use

```bash
usage: vmcheck cluster or vmcheck -o wide cluster

Script to retrieve and display information about VMs for the OpenShift clusters.

Available clusters:
  <cluster1>
  <cluster2>
  <cluster3>
  <cluster4>
  <cluster5>

positional arguments:
  cluster            the cluster to retrieve VMs from

optional arguments:
  -h, --help         show this help message and exit
  -o {default,wide}  the layout of the table (default or wide)
```

Basic:

```
(⎈ $ vmcheck cluster2
VM Name                              CPU Usage (GHz)    Memory Usage (GB)  Power State
---------------------------------  -----------------  -------------------  -------------
debug                                           0.03                 0.44  On
test                                            0                    0     Off
vm-2213                                         0.03                 0.16  On
ocp-i-01.kubelink.lab.io                        0.47                 1.28  On
ocp-i-02.kubelink.lab.io                        0.41                 1.28  On
ocp-i-03.kubelink.lab.io                        0.41                 0.64  On
ocp-w-01.kubelink.lab.io                        0.47                 0.64  On
ocp-w-02.kubelink.lab.io                        0.39                 0.64  On
ocp-m-01.kubelink.lab.io                        4.47                 6.88  On
ocp-m-02.kubelink.lab.io                        6.13                 6.4   On
ocp-m-03.kubelink.lab.io                        4.39                 7.68  On
pxe-kubelink.lab.io                             0.03                 0.16  On
-------------------------------------------------------------------------------
Total CPU usage: 17.23 GHz
Total memory usage: 26.20 GB
Number of VMs: 12
```

Wide:

```
(⎈ $ vmcheck cluster2 -o wide
VM Name                              CPU Usage (GHz)    Memory Usage (GB)  IP Address     Hardware Version    Power State
---------------------------------  -----------------  -------------------  -------------  ------------------  -------------
debug                                           0.05                 0.44  192.168.0.240  vmx-19              On
test                                            0                    0     N/A            vmx-19              Off
vm-2213                                         0.03                 0.08  192.168.0.100  vmx-19              On
ocp-i-01.kubelink.lab.io                        0.47                 0.64  192.168.0.20   vmx-19              On
ocp-i-02.kubelink.lab.io                        0.41                 0.64  192.168.0.21   vmx-19              On
ocp-i-03.kubelink.lab.io                        0.41                 0.96  192.168.0.22   vmx-19              On
ocp-w-01.kubelink.lab.io                        0.44                 0.64  192.168.0.23   vmx-19              On
ocp-w-02.kubelink.lab.io                        0.39                 1.28  192.168.0.24   vmx-19              On
ocp-m-01.kubelink.lab.io                        4.21                 6.72  192.168.0.11   vmx-19              On
ocp-m-02.kubelink.lab.io                        5.82                 6.4   192.168.0.12   vmx-19              On
ocp-m-03.kubelink.lab.io                        3.95                 7.68  192.168.0.13   vmx-19              On
pxe-kubelink.lab.io                             0.03                 0.16  192.168.0.9    vmx-19              On
-------------------------------------------------------------------------------
Total CPU usage: 16.21 GHz
Total memory usage: 25.64 GB
Number of VMs: 12
```