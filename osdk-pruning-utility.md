The `operator-lib` pruning utility lets Go-based Operators clean up, or
prune, objects when they are no longer needed. Operator authors can also
use the utility to create custom hooks and strategies.

About the operator-lib pruning utility
======================================

Objects, such as jobs or pods, are created as a normal part of the
Operator life cycle. If the cluster administrator or the Operator does
not remove these object, they can stay in the cluster and consume
resources.

Previously, the following options were available for pruning unnecessary
objects:

-   Operator authors had to create a unique pruning solution for their
    Operators.

-   Cluster administrators had to clean up objects on their own.

The `operator-lib` [pruning
utility](https://github.com/operator-framework/operator-lib/tree/main/prune)
removes objects from a Kubernetes cluster for a given namespace. The
library was added in version `0.9.0` of the [`operator-lib`
library](https://github.com/operator-framework/operator-lib/releases/tag/v0.9.0)
as part of the Operator Framework.

Pruning utility configuration
=============================

The `operator-lib` pruning utility is written in Go and includes common
pruning strategies for Go-based Operators.

**Example configuration.**

    cfg = Config{
            log:           logf.Log.WithName("prune"),
            DryRun:        false,
            Clientset:     client,
            LabelSelector: "app=<operator_name>",
            Resources: []schema.GroupVersionKind{
                    {Group: "", Version: "", Kind: PodKind},
            },
            Namespaces: []string{"default"},
            Strategy: StrategyConfig{
                    Mode:            MaxCountStrategy,
                    MaxCountSetting: 1,
            },
            PreDeleteHook: myhook,
    }

The pruning utility configuration file defines pruning actions by using
the following fields:

<table>
<colgroup>
<col style="width: 30%" />
<col style="width: 70%" />
</colgroup>
<thead>
<tr class="header">
<th>Configuration field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>log</code></p></td>
<td><p>Logger used to handle library log messages.</p></td>
</tr>
<tr class="even">
<td><p><code>DryRun</code></p></td>
<td><p>Boolean that determines whether resources should be removed. If set to <code>true</code>, the utility runs but does not to remove resources.</p></td>
</tr>
<tr class="odd">
<td><p><code>Clientset</code></p></td>
<td><p>Client-go Kubernetes ClientSet used for Kubernetes API calls.</p></td>
</tr>
<tr class="even">
<td><p><code>LabelSelector</code></p></td>
<td><p>Kubernetes label selector expression used to find resources to prune.</p></td>
</tr>
<tr class="odd">
<td><p><code>Resources</code></p></td>
<td><p>Kubernetes resource kinds. <code>PodKind</code> and <code>JobKind</code> are currently supported.</p></td>
</tr>
<tr class="even">
<td><p><code>Namespaces</code></p></td>
<td><p>List of Kubernetes namespaces to search for resources.</p></td>
</tr>
<tr class="odd">
<td><p><code>Strategy</code></p></td>
<td><p>Pruning strategy to run.</p></td>
</tr>
<tr class="even">
<td><p><code>Strategy.Mode</code></p></td>
<td><p><code>MaxCountStrategy</code>, <code>MaxAgeStrategy</code>, or <code>CustomStrategy</code> are currently supported.</p></td>
</tr>
<tr class="odd">
<td><p><code>Strategy.MaxCountSetting</code></p></td>
<td><p>Integer value for <code>MaxCountStrategy</code> that specifies how many resources should remain after the pruning utility run.</p></td>
</tr>
<tr class="even">
<td><p><code>Strategy.MaxAgeSetting</code></p></td>
<td><p>Go <code>time.Duration</code> string value, such as <code>48h</code>, that specifies the age of resources to prune.</p></td>
</tr>
<tr class="odd">
<td><p><code>Strategy.CustomSettings</code></p></td>
<td><p>Go map of values that can be passed into a custom strategy function.</p></td>
</tr>
<tr class="even">
<td><p><code>PreDeleteHook</code></p></td>
<td><p>Optional: Go function to call before pruning a resource.</p></td>
</tr>
<tr class="odd">
<td><p><code>CustomStrategy</code></p></td>
<td><p>Optional: Go function that implements a custom pruning strategy</p></td>
</tr>
</tbody>
</table>

**Pruning execution.**

You can call the pruning action by running the execute function on the
pruning configuration.

    err := cfg.Execute(ctx)

You can also call a pruning action by using a cron package or by calling
the pruning utility with a triggering event.
