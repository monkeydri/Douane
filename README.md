<p align="center">
  <a href="http://blog.zedroot.org/" target="_blank">
    <img src="https://raw.github.com/zedtux/gpair/master/media/developpeur_breton_logo.png" alt="Je suis un developpeyr Breton!"/>
  </a>
</p>

# Douane

Douane is a firewall that filter and limit the outgoing network traffic per application.

You can allow network traffic for some applications and deny network traffic for others.

### How it works

When Douane is started, it will watch the outgoing network traffic and as soon as an unknown application tries to send some network packets, Douane will block it and ask if you want to allow it or not:

![Douane - Question window](https://pbs.twimg.com/media/BNIv_V2CEAAPPyi.png:large)

The application is composed of multiple parts written in different programming languages.

#### Architecture

This project is divided in multiple pieces in order to make it very flexible. In the following sections, the Git repository of the described part is available in the last line.

If you want to get more information about the Douane architecture, you can have a look at [the Architecture Wiki page](https://github.com/Douane/Douane/wiki/Architecture).

#### Linux kernel module

The [Linux Kernel Module](https://en.wikipedia.org/wiki/Loadable_kernel_module) is the heart of Douane as it will catch outgoing network packets and find the application that sent them.

Written in C, it uses [Netfilter](http://www.netfilter.org/) to watch the network traffic.

The Github repository URL is https://github.com/Douane/douane-dkms.

#### Daemon process

This is the brain of Douane as it will ask you and remember your decisions to allow/deny network traffic.

Written in C++, it provides a [D-Bus](dbus.freedesktop.org/) server in order to communicate with the other parts.

The Github repository URL is https://github.com/Douane/douane-daemon.

#### Dialog processes

The dialog process is the window that appears when an unknown activity has been detected. It is written in [GTK 3](http://www.gtk.org/) for the official project.

The Github repository URL of the Douane version is https://github.com/Douane/douane-dialog. (The dialog process could be written in any language, for any UI, as long as it follows the D-Bus implementation).

#### Configurator

Finally [the configurator](https://github.com/zedtux/douane-configurator) allow you to edit the configuration (rules, load on boot, ...).

![Douane - Configurator](https://pbs.twimg.com/media/BNdVVAOCQAI8CRr.png:large)

The configuration is written in [python 3](http://www.python.org/) and GTK 3 using [PyGObject](https://live.gnome.org/PyGObject), is open source and is an interface to the D-Bus server provided by the daemon process.

The Github repository URL is https://github.com/Douane/douane-configurator. (The configurator process could be written in any language, for any UI, as long as it follows the D-Bus implementation).

### What is supported

The Linux Kernel Module use NetFilter in order to catch the network packets before there are routed. Any packets going through this module are watched by Douane.
Douane is an application firewall preventing unknown applications to send data, so it is outgoing only (as of now) direction. It is simply filtering **userspace** application network traffic based on simple allow/deny rules.
An iptable firewall could be added to dounae in the future. 

**Supported :**
- Any outgoing connection generate by application/library
- Protocols : All (same as NetFilter)
- Direction : Outgoing - Listening

**Not Supported :**
- Non userspace connections : netbios/etc... (Kernel)
- Iptables (not used by douane, but it is recommanded to use it side by side with douane)
- Direction : Incoming (use iptables for that)

### Feature requests and Bug reporting

If you found a bug or have an idea to improve Douane your input is more than welcome!

[Fill in a new Github issue](https://github.com/zedtux/Douane/issues/new) in this project and I will have a look at it.


**For the first release of the application I didn't implement many features in order to keep it as simple as possible in order to focus more on the stability of the application.**

**Now that the application is quite stable (let's see for bug report) I can implement new features so do not hesitate to ask!!**

### Licencing

The entire project is 100% open source under the GPL v2 licence.

### Install

You can find the compilation/installation instructions in [the wiki](https://github.com/Douane/Douane/wiki).
