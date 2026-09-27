# Tailwake

Wake a PC from your iPhone or iPad—on the same local network or through an SSH relay you control.

Tailwake sends a standard Wake-on-LAN (WoL) magic packet. At home, your device broadcasts it directly. Away from home, Tailwake securely connects to an always-on relay device on the PC’s network and asks it to send the wake packet locally.

## Explore Tailwake

- [Instructions](INSTRUCTIONS.md) — Set up local and relay wakes, verification, wake tools, and Siri or Shortcuts.
- [Privacy Policy](PRIVACY.md) — Read how Tailwake handles your information.
- [Terms of Use](TERMS.md) — Review usage and service terms.
- [Support Development](SUPPORT.md) — Learn about the public beta, relay-wake allowance, subscriptions, lifetime unlock, and optional tips.

## Wake your way

On a shared local network, Tailwake sends the magic packet straight from your iPhone or iPad. For a remote wake, it uses an SSH relay device that you choose and control—such as a compatible router or a small Linux computer—on the PC’s network.

> Your remote-access path is your choice. [Tailscale](https://tailscale.com/) is a good way to reach a relay privately without opening an inbound router port.

Tailwake can verify whether a PC is already online, log the result of every wake, and provide a **Wake PC** action for Siri and Shortcuts.

## Private by design

- No account, advertising, analytics, tracking, or developer-run server.
- PC details, relay settings, wake history, and verification results stay on your device.
- SSH credentials and SecureOn passwords are stored in the iOS Keychain.
- Available in English and Traditional Chinese.

Use Tailwake only with computers, networks, and relay accounts that you own or are authorized to control. Wake-on-LAN depends on your hardware, operating-system settings, and network.
