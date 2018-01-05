---
title: calicoctl convert
redirect_from: latest/reference/calicoctl/commands/convert
---

This sections describes the `calicoctl convert` command.

Read the [calicoctl command line interface user reference]({{site.baseurl}}/{{page.version}}/reference/calicoctl/) 
for a full list of calicoctl commands.

> **Note**: The available actions for a specific resource type may be 
> limited based on the datastore used for Calico (etcdv3 / Kubernetes API). 
> Please refer to the 
> [Resources section]({{site.baseurl}}/{{page.version}}/reference/calicoctl/resources/)
> for details about each resource type.
{: .alert .alert-info}


## Displaying the help text for 'calicoctl convert' command

Run `calicoctl convert --help` to display the following help menu for the 
command.

```
Usage:
  calicoctl convert --filename=<FILENAME>
                [--output=<OUTPUT>] [--ignore-validation]

Examples:
  # Convert the contents of policy.yaml to v3 policy.
  calicoctl convert -f ./policy.yaml -o yaml

  # Convert a policy based on the JSON passed into stdin.
  cat policy.json | calicoctl convert -f -

Options:
  -h --help                     Show this screen.
  -f --filename=<FILENAME>      Filename to use to create the resource. If set to
                                "-" loads from stdin.
  -o --output=<OUTPUT FORMAT>   Output format. One of: yaml or json.
                                [Default: yaml]
  --ignore-validation           Skip validation on the converted manifest.


Description:
  Convert config files from Calico v1 to v3 API versions. Both YAML and JSON formats are accepted.

  The default output will be printed to stdout in YAML format.
```

### Examples

```
# Create a set of resources (of mixed type) using the data in resources.yaml.
# Results indicate that 8 resources were successfully created.
$ calicoctl create -f ./resources.yaml
Successfully created 8 resource(s)

# Create the same set of resources reading from stdin.
# Results indicate failure because the first resource (in this case a Profile) 
# already exists.
$ cat resources.yaml | calicoctl apply -f -
Failed to create any resources: resource already exists: Profile(name=profile1)
```

### Options

```
-f --filename=<FILENAME>  Filename to use to create the resource.  If set to
                          "-" loads from stdin.
   --skip-exists          Skip over and treat as successful any attempts to
                          create an entry that already exists.
-n --namespace=<NS>       Namespace of the resource.
                          Only applicable to NetworkPolicy and WorkloadEndpoint.
                          Uses the default namespace if not specified.
```

### General options

```
-c --config=<CONFIG>      Path to the file containing connection
                          configuration in YAML or JSON format.
                          [default: /etc/calico/calicoctl.cfg]
```

## See also

-  [Resources]({{site.baseurl}}/{{page.version}}/reference/calicoctl/resources/) for details on all valid resources, including file format
   and schema
-  [NetworkPolicy]({{site.baseurl}}/{{page.version}}/reference/calicoctl/resources/networkpolicy) for details on the Calico selector-based policy model
-  [calicoctl configuration]({{site.baseurl}}/{{page.version}}/reference/calicoctl/setup) for details on configuring `calicoctl` to access
   the Calico datastore.
