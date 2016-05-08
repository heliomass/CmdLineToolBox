# Mac Toolbox
A collection of small shell scripts which may be useful.

## OS X Verbose Boot Toggle
### Description
A simple script to toggle your Mac's verbose boot mode.

### Usage
Place `verbose_boot_toggle` in your path and then simply run it without arguments to turn verbose boot mode on or off. Note that you will need to supply your root password.

```shell
$ verbose_boot_toggle
You may need to supply your root password to make the change.
Switching verbose boot on.
```

## Magic PWD
### Description
This really exists to solve a personal bugbear I have when I’m `scp`-ing a file from one box to another using an absolute path, and each server's shell is in a different tmux tab. The `pwd` command only gives you the path to the current directory, meaning one has to copy/paste both the directory path *and* the filename between tabs as two separate operations.

`magic_pwd` behaves exactly like `pwd` unless you supply a filename or directory as a final argument, at which point it will display the full path to the destination. It will even provide an error if the path to the destination is invalid, saving you an abortive `scp` operation.

#### Usual Workflow
- Tab 1: Type `pwd`
- Tab 1: Double click on directory path and copy to clipboard
- Tab 2: Paste directory path
- Tab 1: Double click on file name and copy to clipboard
- Tab 2: Paste filename to end of directory path
- Tab 2: Execute command

#### Improved Workflow
- Tab 1: Type `pwd filename.ext`
- Tab 1: Double click on full path to file
- Tab 2: Paste directory path
- Tab 2: execute command

### Usage
Ensure `magic_pwd` is in your path and then alias it to `pwd` in your .bashrc, .zshrc or .profile:

```Shell
[ ! -z "$(which magic_pwd 2> /dev/null)" ] && alias pwd="magic_pwd"
```

#### Regular Usage

```Shell
$ pwd
/Users/heliomass/Projects/settings/scripts/bin
```

### Expanded Usage

```Shell
$ pwd magic_pwd
/Users/heliomass/Projects/settings/scripts/bin/magic_pwd
```

#### Expanded Usage From a Parent Directory

```Shell
$ pwd
/Users/heliomass/Projects/settings
$ pwd scripts/bin/magic_pwd
/Users/heliomass/Projects/settings/scripts/bin/magic_pwd
```