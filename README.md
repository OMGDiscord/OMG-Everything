# 🤖 OMG Everything

<p align="center">
  <img src="./bot-image.jpeg" alt="OMG Everything Bot" width="180" style="border-radius: 50%;">
</p>

<p align="center">
  <strong>The official multi-purpose Discord bot for the SteavenGamerYT Community server.</strong><br>
  Built with <a href="https://discord.js.org/">Discord.js v14</a> and Node.js.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Node.js-18%2B-339933?style=flat&logo=nodedotjs&logoColor=white" alt="Node.js 18+">
  <img src="https://img.shields.io/badge/discord.js-v14.27-5865F2?style=flat&logo=discord&logoColor=white" alt="Discord.js v14">
  <img src="https://img.shields.io/badge/License-ISC-blue.svg?style=flat" alt="License: ISC">
  <img src="https://img.shields.io/badge/Platform-Windows%20%7C%20Linux-lightgrey?style=flat" alt="Platform">
</p>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Key Features](#-key-features)
- [Prerequisites](#-prerequisites)
- [Installation Guide (Windows)](#-installation-guide-windows)
- [Installation Guide (Linux)](#-installation-guide-linux)
- [Discord Developer Portal & Intents](#-discord-developer-portal--intents)
- [Configuration Reference (`.env`)](#-configuration-reference-env)
- [Setting Up Reaction Roles](#-setting-up-reaction-roles)
- [Commands Reference](#-commands-reference)
- [Project Structure](#-project-structure)
- [Troubleshooting & FAQ](#-troubleshooting--faq)
- [License & Author](#-license--author)

---

## 🌟 Overview

**OMG Everything** is a feature-packed Discord bot customized for the SteavenGamerYT community. It handles automated moderation, reaction-based self-roles (color and operating systems), audit logging, link whitelist filtering, attachment archiving, and fun interactive commands.

---

## ⚡ Key Features

- **🛡️ Advanced Moderation & Anti-Spam**:
  - **Smart Swear & Slur Filter**: Detects inappropriate language, Cyrillic lookalikes (homoglyphs), leetspeak substitutions (`@`, `$`, `0`, `!`), and spaced-out bypasses.
  - **Automated Friendly Role Probation**: Users who trigger the swear or excessive caps filter temporarily lose their Friendly role (`ROLE_FRIENDLY_ID`), persisted safely across restarts in `swear_probation.json`.
  - **Link Whitelist Filter**: Restricts links exclusively to approved educational, technical, and media domains (e.g., ArchWiki, Debian, Fedora, GitHub, YouTube).
  - **Anti-Excessive-Caps**: Deletes shout messages containing over 70% capital letters and temporarily revokes the Friendly role.
  - **Channel Chat Guard**: Automatically scrubs unauthorized messages from restricted channels (such as `general-no-chat`) and reposts them cleanly.
- **🎨 Reaction Roles**:
  - **13 Color Roles**: Forest Green, Lime Green, Blood Red, Pikachu, Shroom Pink, Pastel Purple, Joker Purple, Gawdy Yellow, Bright White, Dark Black, Magenta, Good Blue, Royal Blue.
  - **13 OS Roles**: Windows, Linux (Other), Arch, Debian, macOS, Void, Fedora, Gentoo, SteavenLinux, RedHat, OpenSUSE, NixOS, BSD.
  - Dynamic setup commands (`/setupcolors` and `/setuposes`) with support for updating existing message IDs without reposting.
- **📜 Server Audit Logs (`modlogs`)**:
  - Automatically reports member joins, leaves, deleted messages, edited messages, channel creations, channel updates, and channel deletions.
  - Filters out high-frequency bot operations (e.g., DiscordSRV Minecraft bridge updates).
- **💾 Automatic Attachment Archiving**:
  - Mirrors files and images uploaded in channels to a local `uploads/` folder with UUID conflict protection.
- **🎉 Community & Easter Eggs**:
  - `/meme`: Fetches fresh memes from Reddit via Meme API.
  - `@someone`: Defangs `@everyone` and mentions a random server member.
  - Automatic triggers for AFK/BRB notifications, secret songs (`d.mp3`), and video clips (`linuxitandsee.mp4`).

---

## 📦 Prerequisites

Before installing the bot, ensure you have:

1. **Node.js**: Version **18.0.0 or higher** (LTS recommended, Node.js 20+ or 22+).
2. **npm**: Version 9+ (comes bundled with Node.js).
3. **Git**: Installed on your system.
4. **Discord Bot Token**: From the [Discord Developer Portal](https://discord.com/developers/applications).
5. **Discord Developer Mode**: Enabled on your Discord client (`User Settings` > `Advanced` > `Developer Mode`) to copy Server, Channel, and Role IDs.

---

## 🪟 Installation Guide (Windows)

Follow these steps to set up and run the bot on **Windows 10 or 11**:

### Step 1: Install Git & Node.js

1. **Install Node.js (LTS)**:
   - Download the Windows Installer (.msi) from [nodejs.org](https://nodejs.org/).
   - Run the installer and follow the setup wizard (ensure **"Add to PATH"** is selected).
   - Alternatively, install via `winget` in Command Prompt or PowerShell:
     ```cmd
     winget install OpenJS.NodeJS.LTS
     ```
2. **Install Git**:
   - Download Git from [git-scm.com](https://git-scm.com/) or install via winget:
     ```cmd
     winget install Git.Git
     ```
3. Verify your installation by opening a new Command Prompt (`cmd`) and running:
   ```cmd
   node -v
   npm -v
   git --version
   ```

### Step 2: Clone the Repository

Open Command Prompt or PowerShell in your desired folder:

```cmd
git clone https://github.com/OMGDiscord/OMG-Everything.git
cd OMG-Everything
```

*(If you are working inside the `Bot` subdirectory or an existing local clone, navigate directly into that folder).*

### Step 3: Install Dependencies

Run npm to install all required dependencies:

```cmd
npm install
```

### Step 4: Configure Environment Variables

1. Copy the example environment template:
   ```cmd
   copy .env.example .env
   ```
2. Open `.env` in Notepad or VS Code:
   ```cmd
   notepad .env
   ```
3. Fill in your `TOKEN`, channel IDs, and role IDs (see the [Configuration Reference](#-configuration-reference-env) below). Save and close the file.

### Step 5: Start the Bot

You have two options to run the bot on Windows:

- **Option A (Auto-Restart Script)**:
  Double-click `start.cmd` or run in CMD:
  ```cmd
  start.cmd
  ```
  *This batch script automatically restarts the bot if it closes or encounters an unexpected crash.*

- **Option B (Standard NPM / Node)**:
  ```cmd
  npm start
  ```
  *(or `node index.js`)*

### Optional: Run 24/7 in Background on Windows (PM2)

To keep the bot running in the background without keeping a CMD window open:

```cmd
npm install -g pm2
npm install -g pm2-windows-startup
pm2-startup install
pm2 start index.js --name "omg-bot"
pm2 save
```

---

## 🐧 Installation Guide (Linux)

Follow these steps to deploy the bot on a Linux server or desktop (Ubuntu, Debian, Arch Linux, Fedora, CentOS, etc.).

### Step 1: Install Git & Node.js

#### For Ubuntu / Debian / Raspberry Pi OS / Linux Mint:
```bash
# Update package lists
sudo apt update && sudo apt install -y curl git build-essential

# Install Node.js 20.x LTS via NodeSource
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

#### For Arch Linux / Manjaro:
```bash
sudo pacman -Syu --needed nodejs npm git base-devel
```

#### For Fedora / RHEL / AlmaLinux:
```bash
sudo dnf install -y nodejs npm git
```

Verify the installation:
```bash
node -v
npm -v
git --version
```

### Step 2: Clone the Repository

```bash
git clone https://github.com/OMGDiscord/OMG-Everything.git
cd OMG-Everything
```

### Step 3: Install Node Modules

```bash
npm install
```

### Step 4: Configure Environment Variables

1. Copy the example configuration:
   ```bash
   cp .env.example .env
   ```
2. Open `.env` using your preferred terminal editor:
   ```bash
   nano .env
   ```
3. Fill in your `TOKEN` and channel/role IDs. Press `CTRL+O` and `Enter` to save, then `CTRL+X` to exit nano.

### Step 5: Test Run

```bash
npm start
```
Check the console. You should see:
```text
Logged in as OMG Everything#XXXX
Bot is ready!
```
Press `CTRL+C` to stop the test run.

---

### Step 6: Running 24/7 in Background on Linux

#### Option A: Using `systemd` (Recommended for Linux servers)

`systemd` is the standard Linux service manager. It automatically starts your bot on system boot and restarts it on failure.

1. Create a systemd unit file:
   ```bash
   sudo nano /etc/systemd/system/omg-bot.service
   ```
2. Paste the following configuration (replace `your_username` and `/path/to/OMG-Everything` with your actual Linux user and path):
   ```ini
   [Unit]
   Description=OMG Everything Discord Bot
   After=network.target

   [Service]
   Type=simple
   User=your_username
   WorkingDirectory=/path/to/OMG-Everything
   ExecStart=/usr/bin/node index.js
   Restart=always
   RestartSec=10
   Environment=NODE_ENV=production

   [Install]
   WantedBy=multi-user.target
   ```
3. Reload systemd, enable, and start the service:
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable omg-bot
   sudo systemctl start omg-bot
   ```
4. Check the service status and logs:
   ```bash
   # Check status
   sudo systemctl status omg-bot

   # Stream live logs
   journalctl -u omg-bot -f
   ```

#### Option B: Using `PM2` (Process Manager)

If you prefer PM2:
```bash
# Install PM2 globally
sudo npm install -g pm2

# Start the bot
pm2 start index.js --name "omg-bot"

# Save list and enable startup on boot
pm2 save
pm2 startup
# (Run the generated sudo env command printed by PM2)
```

To manage the bot with PM2:
```bash
pm2 status
pm2 logs omg-bot
pm2 restart omg-bot
pm2 stop omg-bot
```

---

## 🔑 Discord Developer Portal & Intents

For the bot to work properly, you **must** configure permissions and Privileged Gateway Intents in Discord's Developer Portal:

1. Go to the [Discord Developer Portal](https://discord.com/developers/applications) and select your application (or click **New Application**).
2. Go to the **Bot** tab on the left:
   - Click **Reset Token** to get your token and paste it into `.env`.
   - Scroll down to **Privileged Gateway Intents** and enable:
     - ✅ **Presence Intent**
     - ✅ **Server Members Intent** *(Required for welcome/leave logs, probation, and role management)*
     - ✅ **Message Content Intent** *(Required to read commands, swear filtering, link filtering, and attachments)*
   - Save Changes.
3. Go to **OAuth2** > **URL Generator**:
   - Under **Scopes**, select: `bot`, `applications.commands`.
   - Under **Bot Permissions**, select:
     - `Administrator` *(recommended for ease of setup)*, OR:
     - `Manage Roles`
     - `Manage Nicknames`
     - `Read Messages / View Channels`
     - `Send Messages`
     - `Manage Messages`
     - `Embed Links`
     - `Attach Files`
     - `Read Message History`
     - `Add Reactions`
4. Copy the generated invite link, open it in your browser, and invite the bot to your Discord server.
5. **CRITICAL - Role Hierarchy**:
   - In your Discord Server Settings > **Roles**, drag the **OMG Everything** role **above** the roles it needs to assign (e.g. above `Friendly`, all color roles, and all OS roles).
   - Discord's permission system prevents bots from managing any role higher than or equal to their highest role.

---

## ⚙️ Configuration Reference (`.env`)

Create a `.env` file in the root directory based on `.env.example`:

| Variable | Description | Example / Note |
|---|---|---|
| `TOKEN` | Discord Bot Application Token | `MTA...` from Discord Developer Portal |
| `GENERAL_CHANNEL_ID` | General conversation channel ID | Main server chat channel |
| `OMG_BOTS_CHANNEL_ID` | Channel where the bot posts its ready message | `#bot-commands` or `#bot-log` |
| `WELCOME_CHANNEL_ID` | Channel ID for welcome messages | `#welcome` |
| `LEAVE_CHANNEL_ID` | Channel ID for goodbye messages | `#goodbyes` |
| `RECTON_ROLES_CHANNEL_ID` | Channel ID where reaction role menus reside | `#roles` or `#reaction-roles` |
| `DISCORD_SRV_BOT_ID` | User ID of DiscordSRV bot (if used) | Ignores channel edit spam from Minecraft bridge |
| `ROLE_FRIENDLY_ID` | Role ID for server "Friendly" members | Automatically removed during swear or caps probation |
| `ROLE_FOREST_GREEN_ID` ... `ROLE_ROYAL_BLUE_ID` | 13 Role IDs for Color self-roles | Created in Server Settings > Roles |
| `ROLE_WINDOWS_ID` ... `ROLE_BSD_ID` | 13 Role IDs for OS self-roles | Created in Server Settings > Roles |

> **Tip**: To copy IDs, enable Developer Mode in Discord (`Settings` > `Advanced` > `Developer Mode`), then right-click any channel, user, or role and click **Copy ID**.

---

## 🎨 Setting Up Reaction Roles

Once your bot is running and invited to your server:

1. Ensure the bot has `Manage Roles` permission and its role is higher than the reaction roles.
2. In your reaction roles channel (matching `RECTON_ROLES_CHANNEL_ID`):
   - Type `/setupcolors` to generate the Color role selection embed and automatic reactions.
   - Type `/setuposes` to generate the Operating System role selection embed and automatic reactions.
3. **Updating an Existing Menu**:
   If you ever modify the role embeds in code and want to refresh an existing message without creating a new one:
   ```text
   /setupcolors <MESSAGE_ID>
   /setuposes <MESSAGE_ID>
   ```

---

## 📖 Commands Reference

### User Commands

| Command | Type | Description |
|---|---|---|
| `/help` | Slash | Displays the general list of bot commands |
| `/ping` | Slash & Prefix | Measures and returns bot latency in milliseconds |
| `/userinfo [target]` | Slash & Prefix | Shows account creation date, avatar, and user ID |
| `/meme` | Slash & Prefix | Pulls and embeds a random meme from Reddit |
| `/upload` | Slash & Prefix | Plays/sends the Enderman secret song (`d.mp3`) |
| `/reasons-why-to-never-upgrade-to-windows-11` | Slash & Prefix | Posts a satirical breakdown of Windows 11 upgrade reasons |
| `@someone` | Text trigger | Mentions a random server member safely without role pings |

### Admin & Staff Commands

| Command | Required Permission | Description |
|---|---|---|
| `/adminhelp` | Everyone | Displays the list of administrative commands |
| `/clear <1-99>` | `Administrator` | Bulk deletes between 1 and 99 messages in the channel |
| `/nicknameremove` | `Manage Nicknames` | Resets custom nicknames for all members across the server |
| `/setupcolors [msg_id]` | `Administrator` | Sends or updates the color reaction role menu |
| `/setuposes [msg_id]` | `Administrator` | Sends or updates the OS reaction role menu |

---

## 📂 Project Structure

```text
OMG-Everything/
├── .env.example            # Environment variables template
├── .gitignore              # Git ignore rules (node_modules, .env, uploads)
├── README.md               # Project documentation and installation guide
├── bot-image.jpeg          # Bot avatar image
├── d.mp3                   # Secret song audio asset
├── index.js                # Core bot application logic and event handlers
├── linuxitandsee.mp4       # Video asset for Linux easter egg
├── package.json            # Project metadata and dependencies
├── package-lock.json       # Locked dependency versions
├── start.cmd               # Windows auto-restarting batch launcher
├── swear_probation.json    # Persistent probation tracking data
└── uploads/                # Directory for archived message attachments
```

---

## ❓ Troubleshooting & FAQ

### 1. `Error: Disallowed Intent(s)`
- **Fix**: Open the [Discord Developer Portal](https://discord.com/developers/applications), select your bot, navigate to the **Bot** tab, and toggle **Server Members Intent** and **Message Content Intent** to **ON**.

### 2. `DiscordAPIError[50013]: Missing Permissions` when giving or removing roles
- **Fix**: Your bot's highest role is lower than the role it is trying to assign. Open **Server Settings** > **Roles**, and drag the bot's role above the reaction and Friendly roles.

### 3. The bot connects, but reaction roles do not react or assign
- **Fix**:
  1. Confirm that `RECTON_ROLES_CHANNEL_ID` in `.env` matches the channel where the message was posted.
  2. Confirm that each role ID in `.env` matches a valid role ID created in your server.

### 4. Node.js syntax error or unsupported features
- **Fix**: Ensure your Node.js version is **v18.0.0 or later** (`node -v`). Discord.js v14 requires modern Node.js features.

---

## 📄 License & Author

- **Author**: [Omar Hany Kasban](https://github.com/omarhanykasban) (SteavenGamerYT)
- **License**: [ISC](LICENSE)
