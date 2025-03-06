# Networking

List interfaces
```bash
ip link
```

List IP address
```bash
ip addr
ip a
```

Set IP address
```bash
ip addr add 192.168.1.10/24 dev eth0
```

View the routing table
```bash
ip route
route
```

Add entries into the routing table
```bash
ip route add 192.168.1.0/24 via 192.168.2.1
```

Check IP forwarding is enabled
```bash
cat /proc/sys/net/ipv4/ip_forward  
#1 => enabled 
#0 => disabled
```