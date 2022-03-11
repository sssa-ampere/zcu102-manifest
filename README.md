# zcu102-manifest

This repository provides Repo manifests to setup the Linux image for the ZCU102 FPGA board used in the [AMPERE project](https://ampere-euproject.eu). It runs on top of Petalinux v2020.2, based on Yocto Zeus.

It is a collection of git repositories known as *layers* each of which provides *recipes* to build software packages as well as configuration information.

Repo is a tool that enables the management of many git repositories given a single manifest file. Tell repo to fetch a manifest from this repository and it will fetch the git repositories specified in the manifest and, by doing so, setup a Yocto Project build environment for you!

## Getting Started

**1.  Install Repo.**

Download the Repo script:

    $ curl https://storage.googleapis.com/git-repo-downloads/repo > repo

Make it executable:

    $ chmod a+x repo

Move it on to your system path:

    $ sudo mv repo /usr/local/bin/

If it is correctly installed, you should see a Usage message when invoked
with the help flag.

    $ repo --help

**2.  Initialize a Repo client.**

Create an empty petalinux project to hold Yocto layers downloaded by the manifest file:

    $ source <path-to-petaLinux>/2020.2/tool/settings.sh
    $ petalinux-create -t project -s  <bsp-file> -n ampere-image 
    $ cd ampere-image
    $ mkdir -p components/ext_source
    $ cd components/ext_source

Tell Repo where to find the manifest:

    $ repo init -u https://github.com/sssa-ampere/zcu102-manifest.git
    $ cd ../..
    $ petalinux-config  --silentconfig

A successful initialization will end with a message stating that Repo is
initialized in your working directory. Your directory should now contain a
.repo directory where repo control files such as the manifest are stored but
you should not need to touch this directory.

To test out a known stable yocto version (example: fido), type:

    $ repo init -u https://github.com/sssa-ampere/zcu102-manifest.git -m meta-xilinx.xml -b fido
    $ repo sync

To get back to the latest master branch, type:

    $ repo init -u https://github.com/sssa-ampere/zcu102-manifest.git -m meta-xilinx.xml -b master
    $ repo sync

To learn more about repo, look at http://source.android.com/source/version-control.html
***

**3.  Fetch all the repositories:**

    $ repo sync

This may take a couple of minutes depending on your connection.

## Staying Up to Date

To pick up the latest changes for all source repositories, run:

    $ repo sync

## Customize

Sooner or later, you'll want to customize the Repo manifest to point at
different repositories and branches or pull in additional meta-layers.

Clone this repository (or fork it on gitenterprise):

    $ git clone https://github.com/sssa-ampere/zcu102-manifest.git

Make your changes (and contribute them back if they are generally useful), and
then re-initialize your repo client

    $ repo init -u <file:///path/to/your/git/repository.git>

## Authors

This manifest file is heavily based on the similar file provided by [Xilinx](https://github.com/Xilinx/yocto-manifests/blob/rel-v2020.2/). The remaning customizations are by:

 - Alexandre Amory (January 2022), [Real-Time Systems Laboratory (ReTiS Lab)](https://retis.santannapisa.it/), [Scuola Superiore Sant'Anna (SSSA)](https://www.santannapisa.it/), Pisa, Italy.

## Funding

This tool has been developed in the context of the [AMPERE project](https://ampere-euproject.eu). This project has received funding from the European Union’s Horizon 2020 research and innovation programme under grant agreement No 871669.
