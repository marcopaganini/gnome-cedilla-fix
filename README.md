# gnome-cedilla-fix

Configure your Gnome "US-International" keyboard layout to generate a cedilla c
(ç) instead of an accented c (ć). This project should be particularly useful to
Brazilian Portuguese users with a US-International layout, but could also be
used by anyone else who needs to constantly type a cedilla c.

## Why do I need this?

The traditional Microsoft "US International" keyboard generates accented
characters by sequences of accent+letter, making text typing easy and familiar
for latin language users. This behavior was translated into X, and then into the
earlier versions of Gnome.

Eventually, most countries defined their own keyboard layouts and Gnome added
full support for those. Unfortunately, at some point during this time, the Gnome
project decided that '+c (accent+c) should generate an accented c instead of a
cedilla c, breaking the widely used US-Intl layout in Gnome for many users.

This move generated substantial frustration, and
[many](https://bugs.launchpad.net/ubuntu/+source/ibus/+bug/518056)
[bugs](http://askubuntu.com/questions/363115/how-to-type-latin-small-letter-c-with-cedilla)
[have](https://ask.fedoraproject.org/en/question/28468/problems-with-letter-c-in-us-international-keyboard-fedora-19/)
[been](http://ubuntuforums.org/showthread.php?t=1851918)
[reported](http://blog.klauskiwi.com/cedilla-c-symbol-using-american-keyboards-in-linux/)
on this topic, without a clear and concise solution. This behavior also causes
confusion when migrating users from other operating systems, and makes Linux
adoption more difficult for those who need to use cedilla-c regularly.

## How do I use this?

At the shell prompt, type:

```bash
$ wget -q https://raw.githubusercontent.com/marcopaganini/gnome-cedilla-fix/master/fix-cedilla -O fix-cedilla
$ chmod 755 fix-cedilla
$ ./fix-cedilla
```

If everything works OK, the program will issue a message indicating the
operation was completed and some tips on how to revert the installation, if
needed.

Make sure to reboot your computer (technically, only a X restart is required) to
activate the changes.

## How does it work?

The program performs two steps:

  * It copies your system "Compose" file into `~/.XCompose` (your personal
    compose file), translating every occurrence of an accented-c (ć) into a
    cedilla c (ç). This should satisfy non-Gnome programs.

  * It configures your environment (in `/etc/environment`) to use the "cedilla"
    module for GTK.

## Compatibility

I've tested this with a few versions of Debian, Ubuntu, and Mint Linux with
success. Please let me know about success and failure stories in other versions
of Linux.

Push requests with fixes and updates are always welcome.
