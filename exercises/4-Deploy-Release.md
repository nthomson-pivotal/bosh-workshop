# BOSH Exercise 4 - Deploy a Release

In this exercise we will deploy an existing Zookeeper release to our BOSH director.

## Get the Manifest File

We will be using an included BOSH manifest file to get started. Download the file from here:

```TODO```

You can open the manifest in your favorite text editor and inspect it.

## Deploy the Manifest

Once you have the manifest locally you can deploy it like so:

```bosh -d zookeeper deploy manifest.yml```

This will:
- Upload the release to the BOSH director
- Deploy Zookeeper to 3 virtual machines

Once the deployment has completed, you can run the smoke tests using the following command:

```bosh -d zookeeper run-errand smoke-tests```

## Inspect Deployment Resources

There are now several commands that can be used to inspect what was deployed.

First, there will now be a BOSH release registered in the director:

```bosh releases```

As well as a deployment:

```bosh deployments```

You can inspect the virtual machines built by BOSH like so:

```bosh vms```

## Upgrade Zookeeper

The next task will illustrate upgrading a deployment, in this case the Zookeeper release we 
previously deployed. Open the `manifest.yml` file for editing and change this line:

```
releases:
- name: zookeeper
  version: 0.0.8
```

So that it reads:

```
releases:
- name: zookeeper
  version: 0.0.9
```

Now deploy the updated manifest file with the same command used to originally deploy:

```bosh -d zookeeper deploy manifest.yml```

## Scaling Zookeeper

A fairly common requirement of infrastructure is to scale horizontally, either adding or
removing instances. In this section we will scale up Zookeeper to 5 instances from its default
3.

Open the `manifest.yml` file for editing and change this line:

```
instance_groups:
- name: zookeeper
  azs: [z1, z2, z3]
  instances: 3
```

So that it reads:

```
instance_groups:
- name: zookeeper
  azs: [z1, z2, z3]
  instances: 5
```

Now deploy the updated manifest file with the same command used to originally deploy:

```bosh -d zookeeper deploy manifest.yml```

## Review BOSH Events

BOSH maintains in internal event log that can be used to review operations that have taken place.
To access the event stream for the Zookeeper deployment execute the following command:

```bosh -d zookeeper events```

Try to tie events in the log to the past exercises that we have gone through to this point.