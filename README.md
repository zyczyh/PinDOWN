# PinDOWN
PinDOWN is a Linux Security Module

The main part of this project is to implementing a linux secure module that we will call
PinDOWN which has the following features:

• PinDOWN identifies programs by their pathname, whereas we can also identifies programs by the

cryptographic hash of their primary binary. In addition to eliminating the need to reading

files and performing hashes within the kernel, this simplification has the benefit of avoiding

the need to deal with scripts (e.g., Python code) and software upgrades. Also, our

PinDOWN uses the pathname of the loaded program and not the cmdline string

in the task struct, which can be manipulated by the process.

• PinDOWN file access control policy is a single program file path stored in the XAttr (extended

attribute) of the protected file's inode. Note that PinDOWN policy does not even specify read and 

write permissions, but rather leaves this distinction to the existing Unix file permissions, 

which is simultaneously enforced.

• PinDOWN does not have a special utility to set file access control policy. It uses Linux's existing 

setfattr and getfattr commands to set and view policy, respectively. For example:

setfattr -n "security.pindown" -v "/usr/bin/mutt\0" /home/enck/.mutt/mutt.passwds

The consequence of this simplification is that any program can call setfattr to change the

policy and access the file. However, this is a course assignment and not a production system.

Note that the "\0" in the above command is to null terminate the value of the xattr when

reading from the kernel.
