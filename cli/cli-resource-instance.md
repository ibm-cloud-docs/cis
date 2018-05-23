---

copyright:
  years: 2018
lastupdated: "2018-05-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Resource Instance

The following `instance` commands are available:

* List CIS Service Instances
* Set Context CIS Service Instance

## List CIS Service Instances
### NAME:
   `instances` - List all CIS service instances.

### USAGE:
   `ibmcloud cis instances`

#### Output:
   * Name
   * Location
   * State
   * Service Name


## Set Context CIS Service Instance
### NAME:
   `instance-set` - Set context service instance to operate.

### USAGE:
   `ibmcloud cis instance-set [INSTANCE_NAME] [--unset]`

### ARGUMENTS:
   `INSTANCE_NAME` is the name of CIS service instance. If it is presented, set the context instance to operate, if not, show the current context instance.

### OPTIONS:
   `--unset`  Unset context instance.
