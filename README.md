# building debian packages for mwlib

## What's this?

This is a small repository containing a collection of shell scripts,
which generate .deb packages for the mwlib python
libraries. [fpm](https://github.com/jordansissel/fpm/) is being used
for this task.

The instructions have been tested on ubuntu 12.04

## Installation

Please install the dependencies by running the following command as
root:

    apt-get install -y rubygems python-dev python-setuptools \
    python-imaging python-lxml python-pygments python-greenlet \
    python-pypdf python-bottle python-pyparsing python-simplejson \
    python-roman libfribidi-dev pkg-config libc-ares-dev libc-ares2 \
    libev-dev libev4 ccache git ocaml-nox

The rest of the installation can be done as a normal user.

First, we configure ruby gem to use --user-install and install
binaries to ~/bin:

    cat >~/.gemrc << EOF
    ---
    install: --no-rdoc --no-ri --user-install --bindir ~/bin
    update:  --no-rdoc --no-ri --user-install --bindir ~/bin
    :verbose: true
    EOF

And install fpm:

    gem install fpm

Clone the repository:

    cd ~; git clone https://github.com/pediapress/mullhase
    export PATH=~/mullhase:~/bin:/usr/lib/ccache:$PATH

Also add the above "export PATH=" line to your .bashrc/.profile.

## Building

Run the following command to build debian packages for all available
package:

	mh-buildall

The result will be copied to `~/mh-root/archive`. This directory can
be configured via environment variable `MH_ROOT`. Take a look at
mh-settings for details.


## TODO

* mark conflict between schmir-texvc and mediawiki-math-texvc
* make "EMBED=0 pyfpm pyzim" work
* find a way to run out testsuites against the installed debian
  packages

