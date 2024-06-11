# logging SSH to discord
![GitHub forks](https://img.shields.io/github/forks/devvyyxyz/modrinth-text-packs)
![GitHub watchers](https://img.shields.io/github/watchers/devvyyxyz/modrinth-text-packs)
![GitHub issues](https://img.shields.io/github/issues-raw/devvyyxyz/modrinth-text-packs)
![GitHub Repo stars](https://img.shields.io/github/stars/devvyyxyz/modrinth-text-packs)
![GitHub repo size](https://img.shields.io/github/repo-size/devvyyxyz/modrinth-text-packs)

This script enhances the functionality of Alexander Henderson's original script for logging SSH sessions to Discord. The original script and blog post can be found [here](https://blog.alexsguardian.net/posts/2022/07/02/LoggingSSHtoDiscord/), and credit goes to Alexander Henderson ([alexandzors](https://github.com/alexandzors)).

## Overview

This Bash script is designed to be added to `/sbin/` and made executable. It integrates with the SSH PAM (Pluggable Authentication Modules) to log SSH session events, such as login and logout, to a Discord channel through a webhook.

## Preview
![Preview GIF](https://s.tigerlake.xyz/r/brave_m3hM2tyzn0.gif?compress=false)

## Installation

1. **Copy the Script:**
   - Copy the script to `/sbin/` and make it executable:
     ```bash
     sudo touch /sbin/sshd-login
     sudo chmod +x /sbin/sshd-discord-login.shsudo chmod +x /sbin/sshd-login
     sudo chown root:root /sbin/sshd-login
     sudo nano /sbin/sshd-login
     ```

2. **Edit PAM Configuration:**
   - Open `/etc/pam.d/sshd` in a text editor.
   - Add the following line to the bottom of the file:
     ```plaintext
     session optional pam_exec.so /sbin/sshd-discord-login.sh
     ```

3. **Set Permissions for Logging:**
   - Ensure the log file has the correct permissions:
     ```bash
     sudo touch /var/log/seen_ips.log
     sudo chmod +x /var/log/seen_ips.log
     sudo chown root:root /var/log/seen_ips.log
     ```

4. **Set Configuration Variables:**
   - Edit the script and set the `WEBHOOK_URL`, `DISCORDUSER`, and `URGENT_ROLE` variables to appropriate values.

5. **Restart SSH Service:**
   - Restart the SSH service for changes to take effect:
     ```bash
     sudo service sshd restart
     ```

## Usage

Once installed, the script will send messages to the configured Discord channel when users log in or out via SSH. It differentiates between new and known remote hosts, providing additional context.

## Credits

- Original script by Alexander Henderson ([alexandzors](https://github.com/alexandzors)): [LoggingSSHtoDiscord](https://blog.alexsguardian.net/posts/2022/07/02/LoggingSSHtoDiscord/)

## Disclaimer

This script is provided as-is without any warranty. Use it at your own risk, and ensure that you comply with your organization's policies and guidelines.

### Donate
<a href="https://www.patreon.com/devvyyxyz" rel="noopener nofollow ugc">
<img src="https://wsrv.nl/?url=https%3A%2F%2Fcdn.jsdelivr.net%2Fnpm%2F%40intergrav%2Fdevins-badges%403%2Fassets%2Fcompact%2Fdonate%2Fpatreon-singular_vector.svg&amp;n=-1" alt="paypal-singular">
</a>
