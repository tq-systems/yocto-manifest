# TQMT1042 repo manifest for the Yocto project build system

This repository provides Repo manifests to setup the Yocto build system for TQ Powerarch modules, starting from the TQMT1042 module generation on.

## Getting started

### Install the repo tool
1. Download the repo tool: `curl http://commondatastorage.googleapis.com/git-repo-downloads/repo > repo`
2. Make it executable: `chmod +x repo`
3. Move it to your system path: `sudo mv repo /usr/local/bin`
4. Verify installation: `repo --help`

### Initialize the repository
1. Create an empty directory: `mkdir yocto && cd yocto`
2. Initialize the repository: `repo init -u ssh://git@github.com/tq-systems/yocto-manifest.git -b jethro-tqmtxxxx`
3. Fetch all the source codes: `repo sync`

### Setup the Yocto project build environment
1. Create an environment file:
    ```
    cat > environment << EOF
    export LOADENV_USER=tq
    export TEMPLATECONF=meta-tq-powerarch/conf
    source poky/oe-init-build-env
    export BB_ENV_EXTRAWHITE="$BB_ENV_EXTRAWHITE FSL_RCW"
	EOF
    ```
2. Load environment: `source environment`

This copies default configuration information into the `build/conf` directory and sets up some environment variables for the build system. This configuration directory is not under revision control; you may wish to edit these configuration files for your specific setup.

### Build an image
After loading the environment, an image can be built e.g. with `bitbake core-image-minimal`.
