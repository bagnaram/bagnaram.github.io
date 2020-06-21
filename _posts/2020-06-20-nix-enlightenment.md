---
layout: post
author: bagnaram
title: "NixOS & Enlightenment"
date: 2020-06-20
---

NixOS is the latest and greatest in terms of system configuration management.
Think of how configuration management tools like Ansible or Packer.io allow you
to define the run-time configuration of you machine in a state-ful way. Combine
that with the power of what is the Nix package manager, and you have a Linux
distribution that follows this model for configuring the entire system.


<img src="/img/desktop.png" alt="desktop" class="inline"/>
My Nixos/Enlighenment desktop.

# NixOS Experience

I decided to test drive NixOS because the idea of defining an entire system
configuration from install as a file sounded like something I wanted to see for
myself. Ideally it would take much of the difficult set-up of many things I
typically maintain such as my [dotfiles](https://github.com/bagnaram/dotfiles/).
These could ideally be managed across systems as a single Nix configuration.

NixOS uses the concept of packages which are layed down over the filesystem.
These packages are stored in the Nix repository **under /nix/**, and are
symlinked over their expected locations on the filesystem. Whenever Nix sets up
your system, it reads through its master configuration file and grabs the
nixpkgs it needs and lays them down in its automated way.

My first install of NixOS was done from a USB drive to my Dell XPS13 machine.
This part was fairly easy using `dd`. The troublesome part was getting the B43
`wl` kernel module to properly detect my wireless device. I don't have access to
a wired ethernet connection, so the only way I am able to install packages from
the Nix repositories was to get wifi working. Out of the box, it didn't so I was
only able to install a fixed set of packages available on the ISO. After some
trial-and-error I found that someone kindly pre-built an older [ISO of
NixOS](https://github.com/NixOS/nixpkgs/issues/15162) containing the required
B43 drivers that would work with my system.

With wifi finally working, it was time to install some packages and come up with my base install. Everything that I need to set-up can be done in the `/etc/nixos/configuration.nix`. This file contains a desired state for which to use the next time I rebuild Nixos. Using the basic configuration template that was installed from the ISO, I was able to modify it to my liking.

```text
  environment.systemPackages = with pkgs; [
    wget
    pciutils
    acpid
    xdotool
    binutils-unwrapped
    vim
    emacs
    iw
    firefox
    lsof
    git
    iosevka
    unzip
    zsh
    i3lock
    libinput-gestures
    enlightenment.terminology
    scrot
  ];
```

Beginning with this vector of packages, I am able to list which packages I would
like installed with my system. Pretty self-explanatory.

```text
fonts.fonts = with pkgs; [
  iosevka
];

```

Moving to fonts, I am an [Iosevka](https://typeof.net/Iosevka/) user, so
installing this is also self-explanatory.

```text

  services.redshift = {
    enable = true;
  };

  location.latitude = 30.26;
  location.longitude =  -97.74;

  # Enable the X11 windowing system.
  services.xserver.enable = true;

  # Enable the Enlightenment Desktop Environment.
  services.xserver.desktopManager.enlightenment.enable = true;
```

For the Enlightenment-related settings, it is simple as toggling a few options.
I decided to use E24 with X11 because Wayland support isn't stable. Redshift is
what I've been using for screen tempurature adjustment. Typically it is a pain
to get set up as a daemon, and in this scenerio, I give it the coordinates, and
enable and it's finished!

```text
# Define a user account. Don't forget to set a password with ‘passwd’.
  users.extraUsers.mbagnara = {
    isNormalUser = true;
    uid = 1000;
    shell = pkgs.zsh;
    home = "/home/mbagnara";
    extraGroups = [
      "wheel"
      "input"
      "bluetooth"
    ];
  };
```

Lastly, I set up my user-acount using the Z-Shell declaratively.

## Conclusion
NixOS isn't without its faults. With ease of configuration, will eventually come
problems in other areas. Specifically I experienced issues upgrading, and issues
debugging applications such as Enlightenment. Because I was installing from an
ISO that was based on Nixos 17, this older version had problems when I tried to
update. I managed to break my system numerous times trying to work through
compatibility problems related to a breaking change in the Nix package. This
change broke the schema for the Nix configuration file, and made it difficult to
perform an update to a newer version.

A solution I managed to get running was to update the Nix package, and side-load
it using the `nix-env` command. It allows packages to be assumed outside of the
current runtime system and it allowed me to update the rest of my packages and
get my system up to the latest stable NixOS release.

# Enlightenment

<img src="/img/icon-enlightenment.png" alt="Enlightenment" class="inline"/>

Enlightenment, or E for short, is a unique piece of software. It is one of the
earliest desktop envionments for the Linux desktop. It has gone through various
iterations, and even experienced a fork at version 16. Enlightenment can be
described as a full feature environment with many bells and whistles while being
visually appealing. However, it doesn't carry the burden of dependencies and
heavy memory usage.

Now I have been using I3 as a tiling window manager on Arch Linux for some time
and I grew accustomed to keyboard-driven navigation. One of the important
features that brought me to try E was its new tiling module. It provides most of
the tiling functionality someone would expect from I3, or Yabai.

## Setup

As mentioned above, Enlightenment is simple to include in the NixOS
configuration because it is already a member of nixpkgs. On bootup, I was
presented with an Enlightenment setup screen on my first login. I was asked to
set up languages, keyboards, and even given the choice between tiling and
standard mode. I filled in this information and was set-up with a new Enlightenment desktop.

If there is any desktop environment you would like to configure and tweak, it
would be enlightenment. While most DEs are fully customizable with
configuration, E takes this a step furtherr and provides a rich set of
customizations and options to configure it to your preference.

<img src="/img/enlightenment-01.png" alt="E Config" class="inline"/>

And you will want to configure Enlightenment from its default. There are small
nuances of the desktop experience I didn't want to give up, and many nice tweaks
to improve workflow. For example, I set up a series of keyboard shortcuts to
switch desktops, and to move focused applications to verious desktops like in
I3.

## Conclusion

Enlightenment is nice. It took some time to customize and work through some
issues. I like its relative obscurity and the community isn't tossed to and fro
from the waves of the sea, like Gnome. Things that I found joy setting up like
ACPI shortcuts for screen brightness and battery notifications were brittle
custom scripts, and these seem to just work with E. Although wifi was tricky
setting up because of b43 drivers, I was able to make use of the up and coming
IWD with Enlightenment's connman wifi selector. It is easy and just works. Not
all applications support EFL, Enlightenments toolkit. This means apps like
Firefox don't maintain the exact styling as native enlightenment, including
cursors. I wish this was more seamless. But overall, E is great, has a great
community.
