# Out-of-tree SWAP with WASP

WASP can be usde in order to grant SWAP to certain containers using
an out-of-(kubernetes)-tree mechanism based on an OCI hook.

The design can be found in https://github.com/openshift/enhancements/pull/1630

# Scope

- Node
  - Enable swap on the node
  - Disable swap in the system.slice
  - Set io latency for system.slice
  - Install an OCI hook to enable swap
  - Set memory.high for kubepods.slice
  - Configure soft eviction
- Workloads
  - Enable swap=max for every burstable pod using an OCI hook
  - Set limited swap for workloads (TODO)

# Build

    $ bash to.sh build
    $ bash to.sh push  # only to my account right now

# Deploy

    # Deploy to OCP 4.15 or higher
    $ oc login --token= …
    $ bash to.sh deploy

# Demo

    $ oc apply -f manifests/static.yaml
    $ oc apply -f manifests/stress.yaml
    # Now increase the stress deployment replicacount in order to push out
    # memory of static pods

# Destroy

    $ bash to.sh destroy
