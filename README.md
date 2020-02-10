# nixpkgs-chromium

(related: [nixpkgs-wayland](https://github.com/colemickens/nixpkgs-wayland)
and [nixpkgs-graphics](https://github.com/colemickens/nixpkgs-graphics))

## Overview

This is a package-set for NixOS or nixpkgs that contains builds of Chromium for Wayland (aka Chromium built with the X11 and Wayland backends for Ozone).

I will try to update and build this 1-4 times a month. Since this is a package set, at worst you'll have
some local bloat, but you won't ever accidentally have to rebuild chromium like might happen with an overlay.

<img src="./chromium.png" />

## Packages

 * `chromium-dev-wayland` - Chromium with Ozone (x11/wayland) and GTK/Glib enabled

## Usage

#### Cachix

See the usage instructions on [nixpkgs-wayland.cachix.org](nixpkgs-wayland.cachix.org) for instructions on how to use the Cachix binary cache so that you don't have to build `chromium-dev-wayland` yourself.

#### Usage

Quick test:

```nix-env -iA chromium-dev-wayland -f "https://github.com/colemickens/nixpkgs-chromium/archive/master.tar.gz"```

Using in your nixos `configuration.nix`:

```nix
{ pkgs, ...}:

let
  chrpkgsBall = builtins.fetchTarball { url = "https://github.com/colemickens/nixpkgs-chromium/archive/master.tar.gz"; };
  chrpkgs = import chrpkgsBall;
in
{
  config = {
    nix = {
      binaryCachePublicKeys = [ "nixpkgs-wayland.cachix.org-1:3lwxaILxMRkVhehr5StQprHdEo4IrE8sRho9R9HOLYA=" ];
      binaryCaches = [ "https://nixpkgs-wayland.cachix.org" ];
    };

    environment.systemPackages = [ chrpkgs.chromium-dev-wayland ];
  };
}
```

## Credit

Credit to @volth for doing the hard work of writing a `chromium-git` derivation: https://github.com/NixOS/nixpkgs/pull/66438

