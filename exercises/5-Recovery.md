# BOSH Exercise 4 - Recovery Mechanisms

In this exercise we will trigger some of the recovery mechanisms in BOSH to see how it responds
to failure scenarios.

## Process Failure

BOSH leverages `monit` to ensure that processes on VMs are recovered on failure. To trigger this
we will SSH in to a VM and simulate a process-level event that will cause that process to recycle.

SSH in to a Zookeeper VM like so:

```bosh -d zookeeper ssh zookeeper/<instance id>```

And review the OS processes that are currently running on that VM related to Zookeeper:

```ps -ef | grep zookeeper```

Now kill the process from the previous command:

```sudo kill -9 <process id>```

If you want several seconds and review `ps` further, you will notice a new process has started in its place.

Exit from the SSH session using the `exit` command, and then re-review `bosh -d zookeeper events`. You will notice
the latest events illustrate BOSH registering the process failure and restarting it.

## VM Failure

BOSH will also automatically attempt to recover VMs that have failed. In this example, we will simulate
a network card failure, which will cause BOSH to lose contact with the agent on that VM and recycle it.

Execute the following command to remotely trigger the failure:

```bosh -d zookeeper ssh zookeeper/<instance id> -c 'sudo ifdown eth0 & exit```

Over the next 10-15 minutes BOSH will detect the failed VM and rebuild it from scratch. You can watch this process unfold
through the `bosh vms` command, as well as watching the `bosh events` log for the Zookeeper deployment.
