Udoo Neo board BSP startup
==========================

To get the BSP you need to have repo installed and use it as:

Install the repo utility
------------------------

::

  $ mkdir ~/bin
  $ curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
  $ chmod a+x ~/bin/repo

Download the BSP source
-----------------------

::

  $ PATH=${PATH}:~/bin
  $ mkdir udoo-neo-bsp
  $ cd udoo-neo-bsp
  $ repo init -u https://github.com/sarnold/foss-udoo-neo-platform-bsp -b poky-morty
  $ repo sync

At the end of the commands you have every metadata you need to start work with.

To start a simple image build for an Udoo Neo full board::

  $ cd poky
  $ source ./oe-init-build-env build-dir  # you choose name of build-dir
  $ ${EDITOR} conf/local.conf             # set MACHINE to XXXX
  $ bitbake core-image-minimal

You can use any directory (build-dir above) to host your build.  The above commands
will build an image for nitrogen6x using the udoo-neo BSP machine config and the
default fsl-linux kernel.

For some machines, you can replace the default fsl kernel with a patched mainline
kernel; see the armv7multi kernel recipes in meta-small-arm-extra (note new machines
will be added as this manifest evolves).

The main source code is checked out in the bsp dir above, and the build output dir
will default to poky/build-dir unless you choose a different path above.

See the default.xml file for repo and branch details; note that krogoth branches
use meta-fsl-arm instead of meta-freescale.

Source code
-----------

Download the manifest source here::

  $ git clone https://github.com/sarnold/foss-udoo-neo-platform-bsp

Using Development and Testing Branches
--------------------------------------

Replace the repo init command above with one of the following:

For developers - pyro

::

  $ repo init -u https://github.com/sarnold/foss-udoo-neo-platform-bsp -b poky-pyro

For intrepid developers and testers - master

Patches are typically merged into master-next and then are merged into master
after a testing and comment period. It’s possible that master has
something you want or need.  But it’s also possible that using master
breaks something that was working before.  Use with caution.

::

  $ repo init -u https://github.com/sarnold/foss-udoo-neo-platform-bsp -b poky-master

