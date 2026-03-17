# Quick Start Guide

To get set up to operate and deploy the RRIV board, you will need to install the `rrivctl` command line tool and set up your computer for USB communication with the RRIV board. You will communicate with the RRIV board using the `rrivctl` command line tool.

The instructions below are for Linux. If you are using MacOS or Windows, some of the installation steps will be different.

## 1. Add Linux Permissions

Add the proper Linux permissions using the commands below in your CLI (command line interface):
```bash
sudo groupadd plugdev
sudo usermod -aG plugdev {username}
sudo usermod -aG dialout {username}
```

Log out/in of Linux or reboot your machine after running these commands.

## 2. Clone Repositories

Clone the necessary repositories from the RRIV Github:

- Repos: `rriv-firmware`, `rriv-ctl`, `rriv-configurations`, and `rriv-scripts`
- Use `git clone` in your CLI

Then, run this command to ensure `rrivctlv2` is installed:
```bash
curl --proto '=https' --tlsv1.2 -LsSf https://github.com/rrivirr/rriv-ctl/releases/latest/download/rrivctl-installer.sh | bash
```

## 3. Download udev Rules

Download the following raw files from the RRIV Github:

- [69-probe-rs.rules](https://github.com/rrivirr/rriv-documentation/blob/main/hardware/udev/69-probe-rs.rules)
- [69-rriv.rules](https://github.com/rrivirr/rriv-documentation/blob/main/hardware/udev/69-rriv.rules)

Copy each file into the proper location using the following command:
```bash
sudo cp {filename} /etc/udev/rules.d/
```

You can verify this worked by navigating to that directory with `cd` and listing files with `ls -l` — both `69-probe-rs.rules` and `69-rriv.rules` should appear.

Then, reload the rules with:
```bash
sudo udevadm control --reload
```

## 4. Install Rust and Dependencies

Navigate to [https://rustup.rs/](https://rustup.rs/) and follow the instructions to download Rust.

After Rust is installed, run each of the following commands:
```bash
rustup toolchain install nightly
rustup target add thumbv7m-none-eabi
rustup default nightly
curl --proto '=https' --tlsv1.2 -LsSf https://github.com/probe-rs/probe-rs/releases/latest/download/probe-rs-tools-installer.sh | sh
```

Rerun `rustup target add thumbv7m-none-eabi` to confirm it has been installed.

## 5. Connect to the Datalogger

Use the following command to connect to the RRIV board:
```bash
rrivctlv2 connect
```

Once connected, navigate to the `/rriv-scripts/probe-rs/` directory and run:
```bash
source clear-eeprom.sh
```

This will reformat the EEPROM on the board before flashing it with the RRIV firmware.

## 6. Install VS Code

Install VS Code using instructions from their [website](https://code.visualstudio.com/).

- Once installed, add the **rust-analyzer** extension
- Connect the J-Link between your machine and the board and test the build by clicking the **Run, Build and Debug** button

## 7. Configure Your Device

Once the board has been flashed with the most up-to-date firmware, follow the steps below:

### New Users

If you have never used the RRIV platform before, register your details:
```bash
rrivctlv2 auth login
```

This will prompt you for your email and password. Then continue with the steps below.

### New and Returning Users
Run each of the commands below in your terminal. This will (1) ensure your software is up to date and (2) register your board with RRIV servers.
```bash
rrivctlv2 update
rrivctlv2 provision device
```

A submenu will appear prompting you to name your device:
```bash
rrivctlv2 connect -a {datalogger name}
```

## Ready to go!
Your board has now been successfully set up and is ready for use! Continue browsing through the documentation to discover configuration settings, commands and use-cases for your datalogger.
