# BOSH Exercise 1 - Setup CLI

In this exercise we will setup local tools to allow us to interact with BOSH and its associated tools.

## Install BOSH CLI

Follow the installation instructions here:

https://bosh.io/docs/cli-v2-install/

## Install CredHub CLI

Follow the installation instructions here:

https://github.com/cloudfoundry-incubator/credhub-cli#installing-the-cli

## Setup Connection Configuration

The leader of the workshop will provide you with a file `bosh-env` that will set up connectivity to BOSH components.

To connect to your BOSH director:
- Place `bosh-env` in a local directory
- From a Linux/Cygwin command-line execute `source bosh-env`
- Test connectivity using the command `bosh vms`