---
layout: post
author: bagnaram
title: "NixOS & Enlightenment"
date: 2020-06-20
---
![nixos]( data:image/png;base64,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)

[NixOS](https://nixos.org/) is the latest and greatest in terms of system
configuration management. Think of how configuration management tools like
Ansible or Packer.io allow you to define the run-time configuration of you
machine in a state-ful way. Combine that with the power of what is the Nix
package manager, and you have a Linux distribution that follows this model for
configuring the entire system.


<a href="/img/desktop.png"><img src="/img/desktop.png" alt="desktop" class="inline"/></a>
My Nixos/Enlightenment desktop.

# NixOS Experience

I decided to test drive NixOS and see what I thought. The idea of defining an
entire system configuration from install in a single place sounded like
something I wanted to see for myself. Ideally, it would take much of the
difficult setup of things I typically maintain separately like my
[dotfiles](https://github.com/bagnaram/dotfiles/). These could ideally be
managed across systems as a single Nix configuration.

NixOS uses the concept of packages which are laid down over the filesystem.
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

Although I didn't get to merge everything from my previous system & dotfiles, I
have a good starting place with NixOS. I have a declarative system that I can
easily tear down and even provision as a VM while keeping my favorite settings.
My dotfiles are still a separate repo, but I am looking at something like [Home
manager](https://nixos.wiki/wiki/Home_Manager) as a drop-in replacement using
its own wrappers. All in all, give Nix a go and see for yourself!

# Enlightenment

<img src="/img/icon-enlightenment.png" alt="Enlightenment" class="inline"/>

[Enlightenment](https://www.enlightenment.org/), or E for short, is a unique
piece of software. It is one of the earliest desktop environments for the Linux
desktop. It has gone through various iterations, and even experienced a fork at
version 16. It has a very colorful history and helped to shape what desktops
could do, using its compositing window manager. There are many outrageous
screenshots of highly customized desktops that may have been more over-the-top
in visuals than usability! However, this demonstration carried Enlightenment
into its relatively niche yet passionate space it finds itself in today.

<img src="/img/enlightenment-02.jpg" alt="E16" class="inline"/>
E16 in its hay-day

Don't worry, I am installing E24, released in early June 2020. Enlightenment can
be described as a full feature environment with many bells and whistles while
being visually appealing. However, it doesn't carry the burden of dependencies
and heavy memory usage.


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
configuration, E takes this a step further and provides a rich set of
customizations and options to configure it to your preference.

<img src="/img/enlightenment-01.png" alt="E Config" class="inline"/>

And you will want to configure Enlightenment from its default. There are small
nuances of the desktop experience I didn't want to give up, and many nice tweaks
to improve workflow. For example, I set up a series of keyboard shortcuts to
switch desktops, and to move focused applications to various desktops like in
I3.

Enlightenment theme icons took some work to get working. Using XDG icon themes
on enlightenment will follow the specification by searching `XDG_DATA_DIRS` for
location of icon themes. Because NixOS handles this directory differently, it
lays down symlinks to the icon package and appends those to the `XDG_DATA_DIRS`
variable. NixOS also forces `mtime` of all its packages to 0, at the time of
writing, breaks how E indexes the icon database. I reached out to IRC, and was
generously helped by one of the E devs Carsten Haitzler with a
[patch](https://github.com/NixOS/nixpkgs/pull/90687)!

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
