<p align="center">
    <a href="https://github.com/techjwalker/reference-sheet/issues">
        <img src="https://img.shields.io/github/issues-raw/techjwalker/reference-sheet.svg?style=flat"
             alt="Issues">
    </a>
    <a href="https://github.com/techjwalker/reference-sheet/pulls">
        <img src="https://img.shields.io/github/issues-pr-raw/techjwalker/reference-sheet.svg?style=flat"
             alt="Pull Requests">
    </a>
    <a href="https://github.com/techjwalker/reference-sheet/graphs/contributors">
        <img src="https://img.shields.io/github/contributors/techjwalker/reference-sheet.svg?style=flat"
             alt="Contributors">
    </a>
    <a href="https://github.com/techjwalker/reference-sheet">
        <img src="https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat"
             alt="Contribs Welcome">
    </a>
</p>
<p align="center">
    <a href="https://tastynode.com">
        <img src="https://img.shields.io/badge/sponsored%20by-tastynode.com-red.svg?style=flat"
             alt="TastyNode.com">
    </a>
</p>

Reference Sheet
=======

A List of Common Commands, Procedures, and Information.

A personal reference sheet (easy copy/paste) and script repository for everything from typical fresh-install commands to complete configurations. Mostly setup for my own use, but feel free to add a pull request if there's anything that should be added or changed.

If you are new to Linux, and are using this reference sheet to help you learn and try new things, try using one of these to test with:

* Easy: [Online Bash Utility](https://www.tutorialspoint.com/execute_bash_online.php)
* Standard: [Git for Windows - With Git Bash](https://git-for-windows.github.io/)
* Advanced: [cygwin - Linux for Windows](https://www.cygwin.com/)

Getting Started
---------------

### Issues

Found an issue with a command, script, or even just some spelling, and aren't able to correct it and submit a pull request yourself?

Log it as an issue, and someone will eventually fix it (likely me).

Something you want to see added, but have no clue how to add it because GitHub is like some advanced nanobiotechnology to you?

Log it as an issue, and someone smarter than you will either add it or tell you they don't care because you're an unsupported lifeform and they haven't updated to the latest version of empathy yet.

### Contributions

Know how to work GitHub like your neighbor works your significant other while you're away at work? Great!

If it's minor, add it right in to the file and submit a pull request on the revision.

Big addition, or change? Fork the whole darn thing and make your changes from the comfort of your own repository before submitting a pull request. Or just keep it to yourself and steal the whole reference sheet, because your parents never loved you as a child, and it's the only way you can feel satisfied anymore.

Common Commands
---------------

This set of common commands are used more frequently, especially when working with a newly installed system. For specific use-case commands, check the corresponding section. If a command is missing here, and seems like it would be beneficial to add, create a pull request to add the changes.

### CentOS

Update, upgrade, clean:
```sh
yum update -y && yum upgrade -y && yum autoremove -y && yum clean all
```

Install Epel, update, upgrade, clean:
```sh
yum install -y epel-release && yum update -y && yum upgrade -y && yum autoremove -y && yum clean all
```

Basic tools install:
```sh
yum install -y wget nano htop bzip2 zip unzip screen
```

Extra tools install:
```sh
yum install -y atop nload smartmontools java
```

Upgrade from minimal install:
```sh
yum groupinstall "Base"
```

List jails (Fail2Ban):
```sh
fail2ban-client status
```

List banned IPs in single jail (Fail2Ban):
```sh
fail2ban-client status JAIL
```

List all banned IPs (Fail2Ban):
```sh
fail2ban-client status | grep "Jail list:" | sed "s/ //g" | awk '{split($2,a,",");for(i in a) system("fail2ban-client status " a[i])}' | grep "Status\|IP list"
```

Unban IP (Fail2Ban):
```sh
fail2ban-client set JAIL unbanip IP
```

### Ubuntu

Update, upgrade, clean:
```sh
apt-get update -y && apt-get upgrade -y && apt-get --purge autoremove -y && apt-get clean
```

Basic tools install:
```sh
apt-get install -y wget nano htop bzip2 zip unzip screen
```

Extra tools install:
```sh
apt-get install -y atop nload smartmontools java
```

List jails (Fail2Ban):
```sh
fail2ban-client status
```

List banned IPs in single jail (Fail2Ban):
```sh
fail2ban-client status JAIL
```

List all banned IPs (Fail2Ban):
```sh
fail2ban-client status | grep "Jail list:" | sed "s/ //g" | awk '{split($2,a,",");for(i in a) system("fail2ban-client status " a[i])}' | grep "Status\|IP list"
```

Simple How-To's
---------------

Information on the basics.

This is the stuff you'll want to commit to memory.

Much of the information listed here is restricted to just the "need-to-know" stuff, rather than having too much information all at once, to help avoid confusion and to make it easier to pick up for beginners.

If there's anything not listed in this section, try a quick Google search for more info.

### Navigation

Check what's in your current directory:
```sh
ls
```

Find the directory you're already in:
```sh
pwd
```

Navigate to a different directory:
```sh
cd folder
```

Navigate to previous directory:
```sh
cd -
```

Navigate up a directory:
```sh
cd ../
```

Navigate to home directory:
```sh
cd ~
```

### File Manipulation

Create a new directory:
```sh
mkdir folder
```

Delete a single file:
```sh
rm file
```

Delete a directory and all contents:
```sh
rm -r folder
```

Delete everything in the current directory without confirmation:
```sh
rm -fr *
```

Move/Rename a file:
```sh
mv file newfile
```

Move/Rename a directory:
```sh
mv folder newfolder
```

Copy a file:
```sh
cp file newfile
```

Copy a directory:
```sh
cp -R folder newfolder
```

### Screens (Multiple Sessions)

Check existing screens:
```sh
screen -ls
```

Start new screen session with name:
```sh
screen -S name
```

Attach to an already running session (if there are multiple screens with the same name, use the output from `screen -ls` to copy the full screen ID):
```sh
screen -x name
```

Detach from current session:
```
Key Combination: CTRL-a d
```

Force the attached session to close completely:
```
Key Combination: CTRL-a
Type :quit then hit Enter
```

NOTE: Closing a screen session does not guarantee that you will close whatever is running within that session.

Use-Case How-To's
---------------

Information on what to do, and what kind of commands to run, in order to accomplish different things in certain scenarios.

Keep in mind there are typically many different ways to do things, and often better than what's suggested here. If you personally know a better solution, mention it in an issue or add it yourself with a pull request.

### Kill a Frozen Process

So something went south, a process caught fire, and now you have 80% memory usage on a process you can't close out of anymore.

Don't worry, here's how you use the fire extinguisher:

First, find the PID of the process. Easiest way is to check `top`.
```sh
top
```

Not sure which one is the right one? Grab the PID of whichever process seems most likely the one you want, then use this:
```sh
ls -l /proc/PID/cwd
```

Replacing PID with the PID you copied from `top`, of course.

This should tell you which folder that process is running from, which should (hopefully) help you verify whether it's the process you need to force close.

Then run this command to kill that process:
```sh
kill -9 PID
```
