---
layout: page
title: Installing the Server and Repo Tools
redirect_from:
 - /wiki/page/Installing_the_Server/Repo_Tools
 - /manual/html_node/System-Requirements.html
 - /manual/html_node/Setup.html

---

The [fdroidserver](https://gitlab.com/fdroid/fdroidserver) tools provide
everything you need to set up and maintain your own repos, run an fdroid
build server, and even host your own website like f-droid.org. The
F-Droid developers mostly work on Debian, Arch, and Ubuntu, so those are
currently the best supported platforms.

In order to setup and maintain your own collection of apps and media,
you need to setup an F-Droid repository using the tools from
*fdroidserver*.

* Do not remove this line (it will not be displayed)
{:toc}


## Debian/Ubuntu/Mint/etc

The F-Droid tools, also known as _fdroidserver_, are
included in recent releases (Debian/jessie, Ubuntu/utopic, and newer).
This should be enough to install the basic F-Droid setup:

    sudo apt-get install fdroidserver


### Older releases

For installing on older releases, there are a couple more simple steps:

-   Ubuntu/Mint: use the [Guardian Project
    PPA](https://launchpad.net/~guardianproject/+archive/ppa/+packages)
    (fingerprint: `6B80 A842 07B3 0AC9 DEE2 35FE F50E ADDD
    2234 F563`):
    ```bash
    sudo add-apt-repository ppa:guardianproject/ppa
    sudo apt-get update
    sudo apt-get install fdroidserver
    ```

-   Debian/wheezy: [setup wheezy-backports](http://backports.debian.org/Instructions/#index2h2),
    then:
    ```bash
    apt-get install fdroidserver/wheezy-backports
    ```


## Apple OSX

You can install `fdroidserver` directly using [MacPorts](https://www.macports.org/ports.php?by=name&substr=fdroidserver), [Homebrew](http://brewformulas.org/Fdroidserver), or `easy_install` as a last resort:

or MacPorts:

```bash
port install fdroidserver
```

or Homebrew:

```bash
brew install android-sdk
android update sdk --no-ui --filter platform-tools,build-tools-22.0.1
brew install fdroidserver
```

With only `easy_install`:

```
sudo easy_install fdroidserver
```


## Windows

### Windows 10 Subsystem for Linux

Starting with the Windows 10 "Anniversary Update", you can [enable an
Ubuntu environment](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)
that runs in Windows, known has "Bash on Windows", "Ubuntu on Windows",
or "Windows Subsystem for Linux".

1.  [setup Windows Subsystem for Linux](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide)
2.  install *fdroidserver* from the [Guardian Project PPA](https://launchpad.net/~guardianproject/+archive/fdroidserver/+packages)
    (fingerprint: `6B80 A842 07B3 0AC9 DEE2 35FE F50E ADDD
    2234 F563`) by running this in the Bash shell window:
```bash
sudo add-apt-repository ppa:guardianproject/fdroidserver
sudo apt-get update
sudo apt-get install fdroidserver
```


### Cygwin

1.  add Java to your PATH:
    <http://www.kingluddite.com/tools/how-do-i-add-java-to-my-windows-path>
2.  Install Cygwin <https://www.sourceware.org/cygwin/>
3.  in Cygwin, install these packages: *gcc-core git openssh python3
    python3-pyasn1 python3-imaging python3-paramiko python3-requests
    python3-setuptools rsync wget*
4.  open a Cygwin bash shell and run: `easy_install fdroidserver`

Then here's the repo setup:

```bash
export ANDROID_HOME=/cygdrive/c/path/to/android-sdk
fdroid init   # the keystore gen will fail
```

After running `fdroid init`, you need to set the Windows path to your
keystore in `config.py`.  It is also possible to install
_fdroidserver_ in a virtual environment using _virtualenv_ and _pip_.


## Installing the latest code (any platform)

The easiest way to install the fdroidserver tools from source is to use
virtualenv and pip. First, make sure you have the Python3 version of
_virtualenv_ or _pyvenv_ installed, it
should be included in your OS's Python distribution or via other
mechanisms like dnf/yum/pacman/emerge/Fink/MacPorts/Brew. Then here's
how to install _fdroidserver_ into a Python "virtual
env":

```bash
git clone https://gitlab.com/fdroid/fdroidserver.git
cd fdroidserver
virtualenv env/  # pyvenv also works
. env/bin/activate
pip3 install -e .
python3 setup.py install
```

## Building apps

To build apps using F-Droid, Java and the whole Android SDK must be
installed.  This process is currently only developed on GNU/Linux, but
we'd love patches getting it working on MacOS and Windows. If you only
want to make F-Droid repositories of APK files that you already have
or don't know what this means, then you can skip this section.

In order to build Android apps with the _fdroidserver_ toolchain,
Java, the Android SDK, and some other essential tools must be
installed.  Only
[parts of the Android SDK](https://qa.debian.org/developer.php?email=android-tools-devel%40lists.alioth.debian.org)
are available in Debian, so the Android SDK must be installed
manually, as well as the packages that it requires (_the Android SDK
tools include some 32-bit binaries, so even 64-bit systems need these
i386 library packages_). The F-Droid tools use the Android SDK to
build and inspect apps, so you must have the Android SDK installed and
setup before using _fdroidserver_.

[Install the Android SDK](https://developer.android.com/sdk/index.html#downloads)
and make sure the `ANDROID_HOME` environment variable is properly
set. Be sure to verify the file you downloaded, you can double-check
the SHA-1 Checksum on Google's download page.

```bash
$ sudo apt-get install openjdk-8-jdk lib32stdc++6 lib32gcc1 lib32z1 lib32ncurses5 ...
$ cd ~
$ wget https://dl.google.com/android/repository/tools_r25.2.3-linux.zip
$ echo "aafe7f28ac51549784efc2f3bdfc620be8a08213  tools_r25.2.3-linux.zip" | sha1sum -c
tools_r25.2.3-linux.zip: OK
$ unzip tools_r25.2.3-linux.zip
$ export USE_SDK_WRAPPER=yes
$ export ANDROID_HOME=~/android-sdk-linux
$ export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
$ android update sdk --no-ui --filter platform-tools,tools,build-tools-25.0.2,android-24
```

To add these settings permanently to your shell:

```bash
$ echo export ANDROID_HOME=$ANDROID_HOME >> .bashrc
$ echo 'export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools' >> .bashrc
```

## Building all apps from f-droid.org

In order to build all apps that are included in f-droid.org, then a
lot more software packages are required:

- all SDK platforms requested by the apps you want to build
- all Debian packages required by every app build process (maven, ant, etc)
- every source code management tool (git, subversion, mercurial, etc)
- every version of the Android NDK that apps use

On top of that, to build apps like they are built on f-droid.org, then
the whole [Build Server Setup](../Build_Server_Setup) is required.
That is a more secure, production-ready setup that requires quite a
bit more setup and resources.  The
[build server provisioning scripts](https://gitlab.com/fdroid/fdroidserver/tree/master/buildserver/)
provide a useful reference for all the needed bits.

If you want to make your own official releases with the F-Droid tools,
then you'll also need to set up the
[Signing Process](../Signing_Process).


## Proprietary, non-free libraries

The Android SDK is made available by Google under a proprietary
license. Within that, the essential build tools, SDK platforms,
support library and some other components are under the Apache license
and source code is provided.

Google APIs, used for building apps using Google Maps, are free to the
extent that the library comes pre-installed on the device.  Google
Play Services, Google Admob, GCM, and many other third party libraries
are proprietary and cannot be included in the main F-Droid repository.
The [MicroG project](https://microg.org) is developing free software
replacements for some of the most used proprietary Google libraries


__TODO__

-   fix `fdroid init --keystore` with Microsoft Windows paths...
