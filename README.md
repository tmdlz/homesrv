# Ubuntu Server Home Lab Setup

Turn an old laptop into a remote-accessible Linux server for Docker and DevOps experiments.

## Prerequisites

- An old PC/laptop with Ubuntu Server installed
- A Mac (or any other machine) for remote access
- A Tailscale account (free)

## 1. Initial SSH Connection

From your Mac, connect to the server on your local network:

<img width="647" height="450" alt="Screenshot 2026-02-01 at 11 11 23 AM" src="https://github.com/user-attachments/assets/5211f212-a854-4aad-b46b-97df2dda1b56" />

Find the server's IP by running `hostname -I` on the server.

## 2. Install Tailscale (Remote Access from Anywhere)

On the server:

```bash
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up
```
<img width="634" height="447" alt="No user sessions are running outdated binaries" src="https://github.com/user-attachments/assets/2b8993c8-0a23-45ba-9056-30e6bb1a094c" />

Copy the authentication URL displayed and open it in your browser to link the device.

Then install Tailscale on your Mac from the [App Store](https://apps.apple.com/app/tailscale/id1475387142) and sign in with the same account.

You can now access your server from anywhere using its Tailscale IP (100.x.x.x).

<img width="551" height="412" alt="tomdaluzeau@gmail com" src="https://github.com/user-attachments/assets/47413266-4a18-4b66-86fe-ea407b885150" />
<img width="934" height="622" alt="Tailscale" src="https://github.com/user-attachments/assets/647cedf9-67eb-4ebd-922e-a1518bd92fac" />

## 3. Enable Services at Boot

Ensure SSH and Tailscale start automatically:

```bash
sudo systemctl enable ssh
sudo systemctl enable tailscaled
```
## 4. Prevent Sleep on Lid Close (Laptops)

Edit the logind configuration:

```bash
sudo nano /etc/systemd/logind.conf
```

Add or uncomment these lines:

```ini
HandleLidSwitch=ignore
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore
```
<img width="680" height="415" alt="Screenshot 2026-02-01 at 11 46 57 AM" src="https://github.com/user-attachments/assets/4667627c-b4a0-4333-bfbb-6d4ff9389c8c" />

Apply the changes:

```bash
sudo systemctl restart systemd-logind
```

You can now close the laptop lid without it going to sleep.

## Quick Connect

Add this alias to your `~/.zshrc` on Mac for easy access:

```bash
alias lab="ssh username@100.x.x.x"
```
## Next Steps

- [ ] Mettre en place l'auth avec ssh







