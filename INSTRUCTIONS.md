# Tailwake instructions

[← Tailwake home](README.md) · [Automate Wakes](AUTOMATION.md) · [Support Development](SUPPORT.md) · [Privacy Policy](PRIVACY.md) · [Terms of Use](TERMS.md)

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

## Wake remotely

A router or small Linux computer on the target PC’s local network can act as an SSH relay. In Tailwake, choose **Relay (SSH)**, then enter the relay device’s address, port, user, authentication method, and wake tool.

The relay device receives the SSH connection from Tailwake and broadcasts the wake packet where the target PC can hear it.

### Router as relay

An SSH-capable router can serve as a relay if it can run the selected wake tool. OpenWrt is a strong choice; Asuswrt-Merlin, FreshTomato, DD-WRT, and Gargoyle can also work when SSH is enabled and the needed wake tool is available.

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

Your relay must be reachable from Tailwake and able to reach the target PC’s local broadcast or VLAN segment. Tailwake can show the commands it uses before you confirm an installation, then offer to install a missing wake tool with the relay device’s package manager. Installation needs internet access and may need root or passwordless `sudo` on the relay device.

### Relay authentication and security

Use an SSH password or an unencrypted OpenSSH Ed25519 private key to sign in to the relay device. The relay device must offer an Ed25519 or ECDSA SSH host key; an RSA-only or otherwise obsolete SSH server must be updated before Tailwake can use it.

Tailwake pins a relay’s SSH host key after its first successful connection. If the key changes later, Tailwake stops before handing over a password or key and asks you to compare the new key before reconnecting.

## Set up a PC in Tailwake

<p align="center">
  <img src="images/example-relay-setup.png" alt="Tailwake Edit PC screen configured for an SSH relay." width="320">
</p>

1. Open Tailwake and add a PC.
2. Enter the PC’s name and MAC address.
3. Choose **Local (UDP)** when you are on the same network, or **Relay (SSH)** for remote wakes.
4. For a relay, enter the SSH connection details, choose password or Ed25519-key authentication, and select `etherwake` or `wakeonlan`.
5. Optionally turn on **Verify** and enter a TCP service on the PC, such as Remote Desktop on port 3389.
6. Test the wake while the PC is still on, before relying on it remotely.

## Verify and log

With **Verify before waking**, Tailwake checks the configured TCP address and port and skips the wake when the PC already answers. **Verify after waking** checks once after the selected 1–60 minute delay (five minutes by default).

The **Wake Log** keeps each wake attempt, follow-up verification, and relay-tool installation result on your device. For waking a PC by voice or on a schedule without opening the app, see [Automate Wakes](AUTOMATION.md).

For relay-wake limits, subscriptions, and optional tips, see [Support Development](SUPPORT.md).
