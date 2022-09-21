# Known issue: SQLite-based `CatalogSource` pod does not become ready due to `Error: open ./db-<number>: permission denied`

Kubernetes started using pod security admission to ensure pod security standards in version 1.24. In OpenShift 4.11, namespaces that are prefixed with `openshift-` do not have restricted pod security enforcement. Restricted enforcement for such namespaces is planned for inclusion in OpenShift 4.12. When restricted enforcement occurs, the security context of the pod specification for catalog source pods must match the `restricted` pod security standard. 

There is a known issue in `opm` that prevents SQLite-based catalog source pods from reaching a `ready` state. ([OCPBUGS-122](https://issues.redhat.com/browse/OCPBUGS-122))

You can verify if you are affected by the known issue by running the following command:

```
$ oc describe pod -n <namespace> <pod_name> | grep Error
```

If you see an error message similar to the following example, your catalog is affected by the bug.

*Example output*

```
Error: open ./db-509442842: permission denied
```

## Workaround 

*Procedure*

- Edit the `CatalogSource` definition by setting the `spec.grpcPodConfig.securityContextConfig` label to `legacy`, as shown in the following example:

```
apiVersion: operators.coreos.com/v1alpha1
kind: CatalogSource
metadata:
  name: my-catsrc
  namespace: my-ns
spec:
  sourceType: grpc
  grpcPodConfig:
    securityContextConfig: legacy
  image: my-image:latest
```

## Adding elevated pod security admission standards to a namespace 

> **Important:** The target namespace must support running pods with the elevated pod security admission standard of `baseline` or `privileged`.

*Procedure* 

1. Turn off the label syncer by adding the `security.openshift.io/scc.podSecurityLabelSync=false` label to the namespace.
2. Apply the pod security admission `pod-security.kubernetes.io/enforce` label. Set the label to `baseline` or `privileged`.

> **Note:** Use the `baseline` pod security policy unless other workloads in the namespace require a `privileged` policy.

*Example `<namespace>.yaml` file*

```
apiVersion: v1
kind: Namespace
metadata:
...
  labels:
    security.openshift.io/scc.podSecurityLabelSync: "false"
    openshift.io/cluster-monitoring: "true"
    pod-security.kubernetes.io/enforce: baseline
  name: "<namespace_name>"
```

### Additional resources

- [Controlling pod security admission synchronization](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.11/html/authentication_and_authorization/understanding-and-managing-pod-security-admission#security-context-constraints-psa-opting_understanding-and-managing-pod-security-admission)

## Preventing the known issue

Catalog authors can prevent the issue from affecting cluster administrators by updating their catalogs to the latest version of `opm` or by migrating their SQLite database catalogs to the file-based catalog format. 

### Updating SQLite-based catalogs to the latest version of `opm`

Catalog authros can update their catalogs to latest version of `opm` that is released with your version of OpenShift Container Platform. Run the following command to update your catalog:

```
$ opm index add --binary-image \
  registry.redhat.io/openshift4/ose-operator-registry:v4.11 \
  --from-index <your_registry_image> \
  --bundles "" -t \<your_registry_image>
```

### Migrating SQLite-based catalogs to the file-based catalog format

> **Important:** The SQLite database format is deprecated, but still supported by Red Hat. In a future release, the SQLite database format will not be supported, and catalogs will need to migrate the file-based catalog format. As of OpenShift Container Platform 4.11, the default Red Hat-provided Operator catalog releases in the file-based catalog format. File-based catalogs are not impacted by this known issue. 

Catalog authors can update their catalog to use the file-based catalog format. 

*Procedure*

- To migrate an SQLite database catalog format to the file-based catalog format, run the following commands:

```
$ opm migrate <registry_image> <fbc_directory>
```

```
$ opm generate dockerfile <fbc_directory> \
  --binary-image \
  registry.redhat.io/openshift4/ose-operator-registry:v4.11
```

The generated Dockerfile can then be built, tagged, and pushed to your registry.
