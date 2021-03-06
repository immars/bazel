---
layout: documentation
title: Installing Bazel on Ubuntu
---

<h1 id="ubuntu">Installing Bazel on Ubuntu</h1>

Supported Ubuntu Linux platforms:

*   18.04 (LTS)
*   16.04 (LTS)

Install Bazel on Ubuntu using one of the following methods:

*   [Use the binary installer (recommended)](#install-with-installer-ubuntu)
*   [Use our custom APT repository](#install-on-ubuntu)
*   [Compile Bazel from source](install-compile-source.md)

Bazel comes with two completion scripts. After installing Bazel, you can:

*   Access the [bash completion script](completion.md#bash)
*   Install the [zsh completion script](completion.md#zsh)

<h2 id="install-with-installer-ubuntu">Installing using binary installer</h2>

The binary installers are on Bazel's [GitHub releases page](https://github.com/bazelbuild/bazel/releases).

The installer contains the Bazel binary. Some additional libraries must also be
installed for Bazel to work.

### Step 1: Install required packages

First, install the prerequisites: `pkg-config`, `zip`, `g++`, `zlib1g-dev`, `unzip`, and `python3`.

```bash
sudo apt-get install pkg-config zip g++ zlib1g-dev unzip python3
```

### Step 2: Download Bazel

Next, download the Bazel binary installer named `bazel-<version>-installer-linux-x86_64.sh`
from the [Bazel releases page on GitHub](https://github.com/bazelbuild/bazel/releases).

### Step 3: Run the installer

Run the Bazel installer as follows:

```bash
chmod +x bazel-<version>-installer-linux-x86_64.sh
./bazel-<version>-installer-linux-x86_64.sh --user
```

The `--user` flag installs Bazel to the `$HOME/bin` directory on your system and
sets the `.bazelrc` path to `$HOME/.bazelrc`. Use the `--help` command to see
additional installation options.

### Step 4: Set up your environment

If you ran the Bazel installer with the `--user` flag as above, the Bazel
executable is installed in your `$HOME/bin` directory. It's a good idea to add
this directory to your default paths, as follows:

```bash
export PATH="$PATH:$HOME/bin"
```

You can also add this command to your `~/.bashrc` file.

<h2 id="install-on-ubuntu"> Using Bazel's APT repository</h2>

### Step 1: Install the JDK (optional)

If you want to build Java code using Bazel, install a JDK:

```bash
# Ubuntu 16.04 (LTS) uses OpenJDK 8 by default:
sudo apt-get install openjdk-8-jdk

# Ubuntu 18.04 (LTS) uses OpenJDK 11 by default:
sudo apt-get install openjdk-11-jdk
```

### Step 2: Add Bazel distribution URI as a package source

**Note:** This is a one-time setup step.

```bash
echo "deb [arch=amd64] https://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list
sudo apt-get install curl
curl https://bazel.build/bazel-release.pub.gpg | sudo apt-key add -
```

If you want to install the testing version of Bazel, replace `stable` with `testing`.

### Step 3: Install and update Bazel

```bash
sudo apt-get update && sudo apt-get install bazel
```

Once installed, you can upgrade to a newer version of Bazel with the following command:

```bash
sudo apt-get install --only-upgrade bazel
```
