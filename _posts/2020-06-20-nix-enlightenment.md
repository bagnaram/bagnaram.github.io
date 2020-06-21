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

# Enlightenment

<img src="/img/icon-enlightenment.png" alt="Enlightenment" class="inline"/>
