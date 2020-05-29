Raspbian Remove Bulky Unneeded Packages
==============================
Raspbian, by default, comes with a bunch of packages pre-installed
that are probably not needed for the typical headless setup / IoT sensor experiment / Pi-Hole DNS server. For example, Wolfram, which is 1 GB by itself. That's quite a lot you're running a 12 GB SD card (the default in my starter kit for Raspberry Pi 4).

Here's how to remove them (on Buster):

	sudo apt-get purge wolfram-engine scratch scratch2 scratch3 nuscratch minecraft-pi sonic-pi dillo gpicview libreoffice*
	sudo apt-get autoremove

Autoremove gets rid of dependencies that are now no longer needed. While you're at it, you might as well clear the local repository (cache):

	sudo apt-get clean

A useful command to look for more optional packages, sorted by size:

	dpkg-query -Wf '${Installed-Size}\t${Package}\t${Priority}\n' | egrep '\s(optional|extra)' | cut -f 1,2 | sort -nr | less

Depending on your config, you may also want to remove Java (openjdk/openjre at ~320 mb) or Chromium (~300 mb).

I started out like this:

    Filesystem      Size  Used Avail Use% Mounted on
    /dev/root        12G   11G  1.1G  91% /

And after cleaning:

    /dev/root        12G  6.4G  5.0G  57% /

