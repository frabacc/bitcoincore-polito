# Building a Bitcoin Core node from scratch (source)

*Guide updated for Bitcoin Core 28.0, December 2024.*

This guide is designed for those who believe in the same values that Bitcoin embodies: control, decentralization, and being aware of the systems you rely on.
By building your Bitcoin node from scratch, you'll not only contribute to the Bitcoin network but also gain deeper insights into how it operates. 
Running a node is an active step towards participating in the Bitcoin philosophy of trustless, decentralized finance.

## Why?

Building a Bitcoin Core node from source allows to have full control over their Bitcoin wallet and to customize its behavior to suit their specific needs.

Running a Bitcoin node has also several perks:

- You can verify your own transactions and blocks indipendently, without trusting a third-party to do it for you
- You will avoid interacting with external services to get information out of the blockchain
- You can support the Bitcoin network, while learning how it works

## Requirements

Before we begin, ensure that your system has the following resources available:

- At least 1 GB of RAM, 350 GB of free space if you plan on running a full-node, and a capable internet connection (500 MB/day of download estimated, 1 GB/day of upload estimated), every OS is supported, and the CPU shouldn't matter (make sure you have at least a dual-core Intel Core i3 equivalent).
- Recommended ones are: 8 GB of RAM, 1TB of hard disk space, a Linux machine (since most distribution have low resource usasge) and a capable ARM or x86 processor.

## Building and installing Bitcoin Core on Linux

### Step 0: Prepare the machine

If you're planning to use the machine only to run a full node, you should install a lightweight Linux distribution, like any Debian-based distro, an example is [LMDE](https://www.linuxmint.com/download_lmde.php) or if you're familiar with working with the command line, you can install Debian Server or any other command line based distros. If you want to run a Bitcoin node on Windows, you may use WSL and run a Debian distribution on Windows.

While having Bitcoin Core running in GUI mode is user-friendly and may help undestanding all the options available, it is not needed for operational use.
Make sure that your user is in the sudoers group. If your user doesn't have admin permissions, or sudo is not installed, execute the following commands:


```
$ su root
<enter root passwd>
# apt-get install sudo
# usermod -aG sudo <username>
# reboot
```

### Step 1: Update your system and install the dependencies

If you're running a Debian/Ubuntu based distro:

```
$ sudo apt update && sudo apt upgrade
```

Install git and the dependencies to compile the source code:

```
$ sudo apt-get install build-essential cmake pkg-config python3 libevent-dev libboost-dev
```

Bitcoin Core comes with a descriptor wallet, and SQLite is required to make it work:

```
$ sudo apt install libsqlite3-dev
```

This will install the new wallet, that stores the transactions in a SQLite3 database. Older versions of Bitcoin Core used Oracle Berkley DB 4.8 to store transactions. If you want to use a legacy wallet, compatible with legacy transactions, you should compile ONLY the the exact version of the Berkley database, following this [guide](https://github.com/bitcoin/bitcoin/blob/master/doc/build-unix.md#berkeley-db). It is not strictly needed.

If you want to run the GUI of Bitcoin Core, you should install the following dependencies:

```
$ sudo apt install qtbase5-dev qttools5-dev qttools5-dev-tools libqrencode-dev
```

If you are using a Desktop Enviroment that uses Wayland as a display server you should install the Wayland QT dependencies:

```
$ sudo apt install qtwayland5
```

## Step 2: Build Bitcoin Core

To build Bitcoin Core clone the repository:

```
$ git clone https://github.com/bitcoin/bitcoin.git
```

Bitcoin Core uses Autogen and make to compile its source code. While the latest build uses cmake, you can still choose to use one of the previous builds by switching the branch. 















