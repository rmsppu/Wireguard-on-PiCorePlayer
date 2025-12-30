# Purpose
Utility scripts, etc for getting wireguard onto a PiCorePlayer instance.

This was inspired by:
  1. an attempt to keep the installation & configuration as self-contained as possible, so it can exist in /home/tc (and be "backed up"), rather than creating a extension
  2. the need to bring the wireguard-tools into picoreplayer version > 8

# Installation
## Store [the file `S99-wireguard`](https://raw.githubusercontent.com/rmsppu/Wireguard-on-PiCorePlayer/refs/heads/main/S99-wireguard) in the default user's home directory as:
```/home/tc/S99-wireguard```

## Login  to the PCP server via `ssh` as the user `tc`

## Ensure `S99-wireguard` is executable with:
```chmod +x /home/tc/S99-wireguard```

## Backup the change to PCP
```pcp bu```

## Execute S99-wireguard at Boot
The file must be executed each time the PCP server boots. This can be done easily by adding `/home/tc/S99-wireguard` as user command via the PCP web gui, through:
>go to the **Tweaks** tab
>
>scroll down to the **User commands** section
>
>add the line:
>
>>`/home/tc/S99-wireguard`
>>
>as one of the three commands

# Usage
The `S99-wireguard` command must be run as root, typically after logging in as the default user (tc) with:
```sudo /home/tc/S99-wireguard```

## Arguments
The `S99-wireguard` command requires one of the options:

**start** start the Wireguard daemon, installing the kernel module and wireguard-tools extension (and dependencies) if needed

**stop** stop the Wireguard daemon, shutdown the `wg0` network interface, remove the configuration file

**status** run the `wg show` command to report on the service status

# To Do
Stop pulling `wireguard-tools` from an older picorelayer repo. Either request that the tools be included with current repos, or build the package following [these commands](http://tinycorelinux.net/11.x/x86_64/tcz/src/wireguard/compile_wireguard-tools) and make the binaries available from this repo.
