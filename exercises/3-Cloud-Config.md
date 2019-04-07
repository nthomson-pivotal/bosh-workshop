# BOSH Exercise 3 - Cloud Config

In this exercise we will work with cloud config of the BOSH director.

## Inspect Cloud Config

The BOSH director that has been set up for you comes with a pre-populated Cloud Config:

```bosh cloud-config```

Look through the output in detail, and see if you can identify what VM types, disk types and 
network information has been set up for your director.

## Update Cloud Config

Now we will update the cloud config applied to your director by adding a new disk type.

First download the cloud config to a local file:

```bosh cloud-config > cloud-config.yml```

Open `cloud-config.yml` in your favorite text editor, and in the section `disk_types` add the 
following:

```
- disk_size: 204800
  name: 200GB
```

Save the file and then execute the following command:

```bosh update-cloud-config cloud-config.yml```

You have now added a new disk type with 200GB that can be used by the VMs we will deploy later.