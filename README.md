# Static_Routing

---

# Static Routing Network Configuration

## Overview

This document provides a detailed configuration of a network topology using static routing. All routes are defined using the subnet mask with the next-hop IP address instead of physical interfaces.

---

## Steps to Configure the Network

### 1. Set Hostnames for Routers

Assign hostnames to all routers using the following commands:

```bash
Router>enable
Router#configure terminal
Router(config)#hostname <hostname>
```

Example for Router 1:
```bash
Router(config)#hostname R1
```

---

### 2. Configure Router Interfaces and Assign IP Addresses

#### **Serial Interfaces**
- **DCE Side:** Configure the clock rate and IP address.
  ```bash
  R4(config)#interface Serial 0/0/0
  R4(config-if)#clock rate 4000000
  R4(config-if)#ip address 5.0.0.1 255.255.255.252
  R4(config-if)#no shutdown
  ```
- **DTE Side:** Assign IP address and enable the interface.
  ```bash
  R5(config)#interface Serial 0/0/0
  R5(config-if)#ip address 5.0.0.2 255.255.255.252
  R5(config-if)#no shutdown
  ```

#### **Gigabit Ethernet Interfaces**
Example for `R1`:
```bash
R1(config)#interface GigabitEthernet 0/1
R1(config-if)#ip address 1.0.0.1 255.255.255.252
R1(config-if)#no shutdown
```

---

### 3. Configure IP Addresses on PCs

1. Open the PC configuration.
2. Navigate to the **Desktop** tab and click on **IP Configuration**.
3. Assign the following:
   - **IP Address:** E.g., `10.1.0.2` for PC0.
   - **Subnet Mask:** `255.255.255.0`.
   - **Default Gateway:** IP address of the connected router interface.

---

### 4. Configure Static Routes

Static routes are defined using the subnet mask and the next-hop IP address instead of the physical interface.

#### **Default Static Routes**
Set a default route to forward packets to the next hop for unknown networks.

Examples:
```bash
R3(config)#ip route 0.0.0.0 0.0.0.0 2.0.0.1
R5(config)#ip route 0.0.0.0 0.0.0.0 5.0.0.1
R6(config)#ip route 0.0.0.0 0.0.0.0 6.0.0.1
```

#### **Specific Static Routes**
Define static routes to known networks.

Examples for `R1`:
```bash
R1(config)#ip route 2.0.0.0 255.255.255.252 1.0.0.2
R1(config)#ip route 10.1.0.0 255.255.255.0 1.0.0.2
R1(config)#ip route 5.0.0.0 255.255.255.252 3.0.0.2
```

Examples for `R2`:
```bash
R2(config)#ip route 10.1.0.0 255.255.255.0 2.0.0.2
R2(config)#ip route 3.0.0.0 255.255.255.252 1.0.0.1
R2(config)#ip route 6.0.0.0 255.255.255.252 4.0.0.2
```

Examples for `R4`:
```bash
R4(config)#ip route 1.0.0.0 255.255.255.252 3.0.0.1
R4(config)#ip route 10.2.0.0 255.255.255.0 6.0.0.2
```

---

### 5. Verification

1. Use the **ping** command to test end-to-end connectivity between devices.
2. Verify all interfaces are operational with `show ip interface brief`.
3. Check routing tables using `show ip route` to confirm the static routes.

---

## Diagram

Refer to the provided `StaticRouting.PNG` file for the network topology and interface connections.

---

