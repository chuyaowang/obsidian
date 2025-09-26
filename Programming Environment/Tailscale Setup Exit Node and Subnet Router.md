# Tailscale

Here’s a structured recap of everything we covered about **Tailscale exit nodes** and related setup:

## 🌐 What is an Exit Node?

- A **Tailscale exit node** is a device in your tailnet that routes _all_ your internet traffic, not just traffic between Tailscale peers.
- It acts like a full‑tunnel VPN gateway: your device encrypts traffic to the exit node, which then forwards it to the wider internet.
- To the outside world, your traffic appears to come from the exit node’s public IP.

---

## ⚙️ What Does It Do?

- **Security**: Protects you on untrusted Wi‑Fi by tunneling all traffic through a trusted machine.
- **Geo‑location**: Lets you appear to be browsing from the exit node’s location.
- **Control**: Ensures all traffic flows through a managed gateway.
- **Convenience**: Still behaves like a normal Tailscale peer (you can SSH, RDP, or serve apps on it).

---

## 🖥️ How to Configure an Exit Node on Linux

1. **Install Tailscale**:
    
    ```bash
    curl -fsSL https://tailscale.com/install.sh | sh
    sudo tailscale up
    ```
    
2. **Advertise as exit node**:
    
    ```bash
    sudo tailscale up --advertise-exit-node
    ```
    
3. **Enable in Admin Console**:  
    In the [Tailscale admin panel](https://login.tailscale.com/admin/welcome), allow that device to be used as an exit node.
4. **Enable IP forwarding** (so it can route traffic):
    
    ```bash
    echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.conf
    echo 'net.ipv6.conf.all.forwarding = 1' | sudo tee -a /etc/sysctl.conf
    sudo sysctl -p
    ```
    

---

## 🖱️ How to Use an Exit Node

- On another device in your tailnet, open Tailscale settings.
- Under **Exit Node**, select the machine you configured.
- Now all your internet traffic is routed through that node.
- You can still SSH into the exit node itself using its Tailscale IP or MagicDNS name.

---

## 🛠️ Configuring a Subnet Router _in Addition_ to an Exit Node

Sometimes you want the exit node to also give access to devices on its local LAN (printers, NAS, IoT devices, etc.).

1. On the exit node, advertise LAN subnets along with exit node capability:
    
    ```bash
    sudo tailscale up --advertise-exit-node --advertise-routes=192.168.1.0/24
    ```
    
    (replace `192.168.1.0/24` with your LAN’s subnet).
2. In the admin console, approve the advertised routes.
3. Now your tailnet devices can:
    - Use the exit node for internet traffic.
    - Reach LAN devices behind it via the advertised subnet.

---

✅ **Summary in one line**:  
A Tailscale exit node is a device that routes all your internet traffic through your tailnet; on Linux you enable it with `--advertise-exit-node` and IP forwarding, you select it from clients to use it, and you can extend it into a **subnet router** by also advertising LAN routes.

---

Would you like me to also draw a **diagram‑style explanation** (text‑based, not visual) showing how traffic flows with and without an exit node + subnet router? That often makes the architecture crystal clear.