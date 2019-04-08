# BOSH Exercise 2 - Upload a Stemcell

In this exercise we will work with stemcells.

## Inspect Stemcells

To check the existing stemcells uploaded the BOSH director, issue the following command:

```bosh stemcells```

As we have not yet uploaded any stemcells, the response will be empty.

## Upload Stemcell

Go to `bosh.io` and obtain a URL for the relevant stemcell based on your IaaS:

Azure: https://bosh.io/stemcells/bosh-azure-hyperv-ubuntu-xenial-go_agent
AWS: https://bosh.io/stemcells/bosh-aws-xen-hvm-ubuntu-xenial-go_agent
GCP: https://bosh.io/stemcells/bosh-google-kvm-ubuntu-xenial-go_agent

Then issue the command to upload the particular stemcell to the BOSH director. An example for Azure
would look like:

`bosh upload-stemcell --sha1 6432f6f83239a3c8383e05d397ee04d06aae729e \
  https://bosh.io/d/stemcells/bosh-azure-hyperv-ubuntu-xenial-go_agent?v=250.25`

If the IaaS you are using does not support Light stemcells (Azure, vSphere, OpenStack), this operation may take a while.

Once the upload has completed, you can again inspect the stemcells on the director to confirm it is present:

bosh stemcells
