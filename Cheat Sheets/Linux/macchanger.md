# macchanger
#linux #MACaddress

To check network devices data:
```shell
ip link show
```

To change MAC address of a device using `macchanger`:
```shell
sudo macchanger --mac=XX:XX:XX:XX:XX:XX device
```

For instance, device is `wlp1s0` shows following properties with `ip link show`:
```text
wlp1s0: <BROADCAST,MULTICAST> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default qlen 1000 link/ether 7a:0a:e5:5e:ea:6d brd ff:ff:ff:ff:ff:ff permaddr 28:cd:c4:66:24:fb
```

Let's change it to `F4:5C:89:A8:1E:59` using `macchanger`:
```shell
sudo macchanger --mac=F4:5C:89:A8:1E:59 wlp1s0
```

Output is:
```text
Current MAC:   7a:0a:e5:5e:ea:6d (unknown)
Permanent MAC: 28:cd:c4:66:24:fb (unknown)
New MAC:       f4:5c:89:a8:1e:59 (unknown)
```

`ip link show` gives following information:
```text
wlp1s0: <BROADCAST,MULTICAST> mtu 1500 qdisc noqueue state DOWN mode DEFAULT group default qlen 1000 link/ether f4:5c:89:a8:1e:59 brd ff:ff:ff:ff:ff:ff permaddr 28:cd:c4:66:24:fb
```