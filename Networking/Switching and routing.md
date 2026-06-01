# 🌐 Switching & Routing

## 🔀 Switching

Switching is how two devices communicate **within the same network** through a switch.

```
A (eth0)                 Switch               B (eth0)
192.168.1.10  ─────────── 192.168.1.0 ─────── 192.168.1.11
```

### Step 1 — Check the network interface is UP

```bash
ip link
# Output:
# eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel
#       state UP mode DEFAULT group default qlen 1000
```

> `UP` in the output means the interface is active.

### Step 2 — Assign an IP address to the interface

```bash
# On System A
ip addr add 192.168.1.10/24 dev eth0

# On System B
ip addr add 192.168.1.11/24 dev eth0
```

### Step 3 — Verify connectivity

```bash
ping 192.168.1.11
# Reply from 192.168.1.11: bytes=32 time=4ms TTL=117  ✅
```

> Both systems are on the same network `192.168.1.0` — the switch handles delivery.

---

## 🔁 Routing

Routing is how devices communicate **across different networks** through a router.

```
Network 1 (192.168.1.0)          Router           Network 2 (192.168.2.0)
A: 192.168.1.10                ┌───────┐           C: 192.168.2.10
B: 192.168.1.11 ───────────── │192.168.1.1 │192.168.2.1│ ─── D: 192.168.2.11
                               └───────┘
```

The router has **two IPs** — one on each network (`192.168.1.1` and `192.168.2.1`).

> 💡 **When System B wants to send a packet to System C — how does it know where the router is?**
> Answer: You tell it using the routing table.

### View the routing table

```bash
ip route
# OR
route
# Output: Kernel IP routing table
# Destination    Gateway        Genmask         Flags  Iface
```

### Add a route — tell System B how to reach Network 2

```bash
ip route add 192.168.2.0/24 via 192.168.1.1
#             ↑ destination     ↑ gateway (router IP on this side)
```

> This tells the system: "To reach the `192.168.2.0` network, send traffic through the gateway at `192.168.1.1`"

---

## 🚪 Gateway

The **gateway** is the door between two networks — the router IP your system uses to exit its own network.

```bash
# From System C (192.168.2.10) — to reach Network 1
ip route add 192.168.1.0/24 via 192.168.2.1
```

---

## 🌍 Default Gateway

When a system doesn't know which specific route to use for a destination, it falls back to the **default gateway** — sends ALL unknown traffic there.

```
Internet clouds: 172.217.194.0 / 216.134.45.0 / 16.44.53.0
          ↑ You can't add a route for every internet address
          ↑ So you set ONE default gateway to handle everything unknown
```

```bash
# Add a specific route
ip route add 192.168.1.0/24 via 192.168.2.1

# Add default gateway — catches ALL unknown destinations
ip route add default via 192.168.2.1
```

### Routing table after setting default gateway

```
Kernel IP routing table
Destination      Gateway        Genmask          Flags  Iface
192.168.1.0      192.168.2.1    255.255.255.0    UG     eth0
172.217.194.0    192.168.2.1    255.255.255.0    UG     eth0
default          192.168.2.1    255.255.255.0    UG     eth0
```

> Any request to a network outside your existing routes → goes to the default gateway.

---

## 📡 IP Forwarding

For a Linux machine to act as a **router** (forward packets between networks), IP forwarding must be enabled.

```bash
# Check if IP forwarding is enabled
cat /proc/sys/net/ipv4/ip_forward
# 1 = enabled  ✅
# 0 = disabled ❌

# Enable IP forwarding (temporary)
echo 1 > /proc/sys/net/ipv4/ip_forward

# Enable permanently (add to /etc/sysctl.conf)
net.ipv4.ip_forward = 1
```

---

## 🧠 Quick Reference

| Command | What It Does |
|---------|-------------|
| `ip link` | Check if network interface is UP |
| `ip addr` | View IP addresses on all interfaces |
| `ip addr add 192.168.1.10/24 dev eth0` | Assign IP to an interface |
| `ip route` | View the routing table |
| `route` | View routing table (older command) |
| `ip route add 192.168.2.0/24 via 192.168.1.1` | Add a route to a specific network |
| `ip route add default via 192.168.2.1` | Set the default gateway |
| `cat /proc/sys/net/ipv4/ip_forward` | Check if IP forwarding is enabled |

---

> 💡 **Tips**
> - **Switching** = same network, no routing needed
> - **Routing** = different networks, need a router + routes configured
> - **Gateway** = the router IP your system exits through
> - **Default gateway** = catch-all for any unknown destination
> - `ip route add default` saves you from adding a route for every internet address
> - If a Linux box is acting as a router, always check `ip_forward = 1`
