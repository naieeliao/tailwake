# Tailwake instructions

[← Tailwake home](README.md) · [Support Development](SUPPORT.md) · [Privacy Policy](PRIVACY.md) · [Terms of Use](TERMS.md)

## Before you start

You need:

- An iPhone or iPad running iOS 17 or later
- A target PC and network adapter that support Wake-on-LAN
- The target PC’s MAC address
- For remote wakes, an SSH-capable relay device on the target PC’s local network

Enable Wake-on-LAN in the target PC’s firmware and operating-system settings before adding it to Tailwake.

Tailwake asks for **Local Network** access to send local wakes. Notifications are optional, but they let Tailwake report that a wake was sent, failed, or was later verified.

## Wake from the same network

When your iPhone or iPad and the target PC share a local network, choose **Local (UDP)** when adding the PC. Tailwake broadcasts the WoL magic packet directly—no relay is required.

<img src="images/direct-udp-broadcast.png" alt="An iPhone or iPad sends a Wake-on-LAN magic packet through the local network to the target computer." width="900">

## Wake while away from home

A router or small Linux computer on the target PC’s local network can act as an SSH relay. In Tailwake, choose **Relay (SSH)**, then enter the relay device’s address, port, user, authentication method, and wake tool.

The relay device receives the SSH connection from Tailwake and broadcasts the wake packet where the target PC can hear it.

### Router as relay

An SSH-capable router can work when it can run the selected wake tool. OpenWrt is a strong choice; Asuswrt-Merlin, FreshTomato, DD-WRT, and Gargoyle can also work when SSH is enabled and the needed wake tool is available.

<img src="images/router-relay-etherwake.png" alt="Tailwake connects over SSH to a router, which sends an Ethernet wake frame to the target computer with etherwake." width="900">

<img src="images/router-relay-wakeonlan.png" alt="Tailwake connects over SSH to a router, which broadcasts a Wake-on-LAN packet to the target computer with wakeonlan." width="900">

### Small Linux computer as relay

A Raspberry Pi is one option, but any always-on Linux single-board computer can work when it has SSH, the wake tool, and access to the target PC’s local broadcast or VLAN segment.

<img src="images/small-computer-relay-etherwake.png" alt="Tailwake connects over SSH to a small Linux computer, which sends an Ethernet wake frame to the target computer with etherwake." width="900">

<img src="images/small-computer-relay-wakeonlan.png" alt="Tailwake connects over SSH to a small Linux computer, which broadcasts a Wake-on-LAN packet to the target computer with wakeonlan." width="900">

### Choose the relay’s wake tool

| Tool | What it sends | What the relay needs |
| --- | --- | --- |
| `etherwake` | A raw Ethernet frame | Root access and the local network interface; supports SecureOn |
| `wakeonlan` | A UDP WoL magic packet | No root access or interface selection; does not support SecureOn |

Whichever relay you use needs SSH access from Tailwake and access to the target PC’s local broadcast or VLAN segment. Tailwake can show the commands it uses and, after your confirmation, offer to install a missing wake tool with the relay device’s package manager. Installation needs internet access and may need root or passwordless `sudo` on the relay device.

### Relay authentication and security

Tailwake supports SSH password authentication and unencrypted OpenSSH Ed25519 private keys. The relay device must offer an Ed25519 or ECDSA SSH host key; an RSA-only or otherwise obsolete SSH server must be updated before Tailwake can use it.

On a relay’s first successful connection, Tailwake pins its SSH host key. If that key changes later, Tailwake stops before handing over a password or key and asks you to compare the new identity before reconnecting.

## Set up a PC in Tailwake

1. Open Tailwake and add a PC.
2. Enter the PC’s name and MAC address.
3. Choose **Local (UDP)** when you are on the same network, or **Relay (SSH)** for remote wakes.
4. For a relay, enter the SSH connection details, choose password or Ed25519-key authentication, and select `etherwake` or `wakeonlan`.
5. Optionally turn on **Verify** and enter a TCP service on the PC, such as Remote Desktop on port 3389. Tailwake can skip a wake when the PC is already online and check once after a wake.
6. Test the wake while the PC is still on, before relying on it remotely.

## Verify, log, and automate

With **Verify before waking**, Tailwake checks the configured TCP address and port and skips the wake when the PC already answers. With **Verify after waking**, it checks once after the selected 1–60 minute delay (five minutes by default). A reply confirms that service is online; no reply does not necessarily mean the PC is off.

The **Wake Log** keeps each wake attempt, follow-up verification, and relay-tool installation result on your device. You can also use the **Wake PC** action from Siri or Shortcuts to wake one of your saved PCs without opening the app.

For relay-wake limits, subscriptions, and optional tips, see [Support Development](SUPPORT.md).
