The Operator SDK command-line interface (CLI) is a development kit designed to make writing Operators easier.

**Operator SDK CLI syntax**

    $ operator-sdk <command> [<subcommand>] [<argument>] [<flags>]

See [Developing Operators](../../operators/operator_sdk/osdk-about.xml#osdk-about) for full documentation on the Operator SDK.

# bundle

The `operator-sdk bundle` command manages Operator bundle metadata.

## validate

The `bundle validate` subcommand validates an Operator bundle.

<table><caption><code>bundle validate</code> flags</caption><colgroup><col style="width: 25%" /><col style="width: 75%" /></colgroup><thead><tr class="header"><th style="text-align: left;">Flag</th><th style="text-align: left;">Description</th></tr></thead><tbody><tr class="odd"><td style="text-align: left;"><p><code>-h</code>, <code>--help</code></p></td><td style="text-align: left;"><p>Help output for the <code>bundle validate</code> subcommand.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--index-builder</code> (string)</p></td><td style="text-align: left;"><p>Tool to pull and unpack bundle images. Only used when validating a bundle image. Available options are <code>docker</code>, which is the default, <code>podman</code>, or <code>none</code>.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>--list-optional</code></p></td><td style="text-align: left;"><p>List all optional validators available. When set, no validators are run.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--select-optional</code> (string)</p></td><td style="text-align: left;"><p>Label selector to select optional validators to run. When run with the <code>--list-optional</code> flag, lists available optional validators.</p></td></tr></tbody></table>

`bundle validate` flags

# cleanup

The `operator-sdk cleanup` command destroys and removes resources that were created for an Operator that was deployed with the `run` command.

<table><caption><code>cleanup</code> flags</caption><colgroup><col style="width: 25%" /><col style="width: 75%" /></colgroup><thead><tr class="header"><th style="text-align: left;">Flag</th><th style="text-align: left;">Description</th></tr></thead><tbody><tr class="odd"><td style="text-align: left;"><p><code>-h</code>, <code>--help</code></p></td><td style="text-align: left;"><p>Help output for the <code>run bundle</code> subcommand.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--kubeconfig</code> (string)</p></td><td style="text-align: left;"><p>Path to the <code>kubeconfig</code> file to use for CLI requests.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>n</code>, <code>--namespace</code> (string)</p></td><td style="text-align: left;"><p>If present, namespace in which to run the CLI request.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--timeout &lt;duration&gt;</code></p></td><td style="text-align: left;"><p>Time to wait for the command to complete before failing. The default value is <code>2m0s</code>.</p></td></tr></tbody></table>

`cleanup` flags

# completion

The `operator-sdk completion` command generates shell completions to make issuing CLI commands quicker and easier.

<table><caption><code>completion</code> subcommands</caption><colgroup><col style="width: 25%" /><col style="width: 75%" /></colgroup><thead><tr class="header"><th style="text-align: left;">Subcommand</th><th style="text-align: left;">Description</th></tr></thead><tbody><tr class="odd"><td style="text-align: left;"><p><code>bash</code></p></td><td style="text-align: left;"><p>Generate bash completions.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>zsh</code></p></td><td style="text-align: left;"><p>Generate zsh completions.</p></td></tr></tbody></table>

`completion` subcommands

<table><caption><code>completion</code> flags</caption><colgroup><col style="width: 25%" /><col style="width: 75%" /></colgroup><thead><tr class="header"><th style="text-align: left;">Flag</th><th style="text-align: left;">Description</th></tr></thead><tbody><tr class="odd"><td style="text-align: left;"><p><code>-h, --help</code></p></td><td style="text-align: left;"><p>Usage help output.</p></td></tr></tbody></table>

`completion` flags

For example:

    $ operator-sdk completion bash

**Example output**

    # bash completion for operator-sdk                         -*- shell-script -*-
    ...
    # ex: ts=4 sw=4 et filetype=sh

# create

The `operator-sdk create` command is used to create, or *scaffold*, a Kubernetes API.

## api

The `create api` subcommand scaffolds a Kubernetes API. The subcommand must be run in a project that was initialized with the `init` command.

<table><caption><code>create api</code> flags</caption><colgroup><col style="width: 25%" /><col style="width: 75%" /></colgroup><thead><tr class="header"><th style="text-align: left;">Flag</th><th style="text-align: left;">Description</th></tr></thead><tbody><tr class="odd"><td style="text-align: left;"><p><code>-h</code>, <code>--help</code></p></td><td style="text-align: left;"><p>Help output for the <code>run bundle</code> subcommand.</p></td></tr></tbody></table>

`create api` flags

# generate

The `operator-sdk generate` command invokes a specific generator to generate code or manifests.

## bundle

The `generate bundle` subcommand generates a set of bundle manifests, metadata, and a `bundle.Dockerfile` file for your Operator project.

Typically, you run the `generate kustomize manifests` subcommand first to generate the input [Kustomize](https://kustomize.io/) bases that are used by the `generate bundle` subcommand. However, you can use the `make bundle` command in an initialized project to automate running these commands in sequence.

<table><caption><code>generate bundle</code> flags</caption><colgroup><col style="width: 25%" /><col style="width: 75%" /></colgroup><thead><tr class="header"><th style="text-align: left;">Flag</th><th style="text-align: left;">Description</th></tr></thead><tbody><tr class="odd"><td style="text-align: left;"><p><code>--channels</code> (string)</p></td><td style="text-align: left;"><p>Comma-separated list of channels to which the bundle belongs. The default value is <code>alpha</code>.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--crds-dir</code> (string)</p></td><td style="text-align: left;"><p>Root directory for <code>CustomResoureDefinition</code> manifests.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>--default-channel</code> (string)</p></td><td style="text-align: left;"><p>The default channel for the bundle.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--deploy-dir</code> (string)</p></td><td style="text-align: left;"><p>Root directory for Operator manifests, such as deployments and RBAC. This directory is different from the directory passed to the <code>--input-dir</code> flag.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>-h</code>, <code>--help</code></p></td><td style="text-align: left;"><p>Help for <code>generate bundle</code></p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--input-dir</code> (string)</p></td><td style="text-align: left;"><p>Directory from which to read an existing bundle. This directory is the parent of your bundle <code>manifests</code> directory and is different from the <code>--deploy-dir</code> directory.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>--kustomize-dir</code> (string)</p></td><td style="text-align: left;"><p>Directory containing Kustomize bases and a <code>kustomization.yaml</code> file for bundle manifests. The default path is <code>config/manifests</code>.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--manifests</code></p></td><td style="text-align: left;"><p>Generate bundle manifests.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>--metadata</code></p></td><td style="text-align: left;"><p>Generate bundle metadata and Dockerfile.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--output-dir</code> (string)</p></td><td style="text-align: left;"><p>Directory to write the bundle to.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>--overwrite</code></p></td><td style="text-align: left;"><p>Overwrite the bundle metadata and Dockerfile if they exist. The default value is <code>true</code>.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--package</code> (string)</p></td><td style="text-align: left;"><p>Package name for the bundle.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>-q</code>, <code>--quiet</code></p></td><td style="text-align: left;"><p>Run in quiet mode.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--stdout</code></p></td><td style="text-align: left;"><p>Write bundle manifest to standard out.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>--version</code> (string)</p></td><td style="text-align: left;"><p>Semantic version of the Operator in the generated bundle. Set only when creating a new bundle or upgrading the Operator.</p></td></tr></tbody></table>

`generate bundle` flags

-   See [Bundling an Operator and deploying with Operator Lifecycle Manager](../../operators/operator_sdk/osdk-working-bundle-images.xml#osdk-bundle-deploy-olm_osdk-working-bundle-images) for a full procedure that includes using the `make bundle` command to call the `generate bundle` subcommand.

## kustomize

The `generate kustomize` subcommand contains subcommands that generate [Kustomize](https://kustomize.io/) data for the Operator.

### manifests

The `generate kustomize manifests` subcommand generates or regenerates Kustomize bases and a `kustomization.yaml` file in the `config/manifests` directory, which are used to build bundle manifests by other Operator SDK commands. This command interactively asks for UI metadata, an important component of manifest bases, by default unless a base already exists or you set the `--interactive=false` flag.

<table><caption><code>generate kustomize manifests</code> flags</caption><colgroup><col style="width: 25%" /><col style="width: 75%" /></colgroup><thead><tr class="header"><th style="text-align: left;">Flag</th><th style="text-align: left;">Description</th></tr></thead><tbody><tr class="odd"><td style="text-align: left;"><p><code>--apis-dir</code> (string)</p></td><td style="text-align: left;"><p>Root directory for API type definitions.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>-h</code>, <code>--help</code></p></td><td style="text-align: left;"><p>Help for <code>generate kustomize manifests</code>.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>--input-dir</code> (string)</p></td><td style="text-align: left;"><p>Directory containing existing Kustomize files.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--interactive</code></p></td><td style="text-align: left;"><p>When set to <code>false</code>, if no Kustomize base exists, an interactive command prompt is presented to accept custom metadata.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>--output-dir</code> (string)</p></td><td style="text-align: left;"><p>Directory where to write Kustomize files.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--package</code> (string)</p></td><td style="text-align: left;"><p>Package name.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>-q</code>, <code>--quiet</code></p></td><td style="text-align: left;"><p>Run in quiet mode.</p></td></tr></tbody></table>

`generate kustomize manifests` flags

# init

The `operator-sdk init` command initializes an Operator project and generates, or *scaffolds*, a default project directory layout for the given plug-in.

This command writes the following files:

-   Boilerplate license file

-   `PROJECT` file with the domain and repository

-   `Makefile` to build the project

-   `go.mod` file with project dependencies

-   `kustomization.yaml` file for customizing manifests

-   Patch file for customizing images for manager manifests

-   Patch file for enabling Prometheus metrics

-   `main.go` file to run

<table><caption><code>init</code> flags</caption><colgroup><col style="width: 25%" /><col style="width: 75%" /></colgroup><thead><tr class="header"><th style="text-align: left;">Flag</th><th style="text-align: left;">Description</th></tr></thead><tbody><tr class="odd"><td style="text-align: left;"><p><code>--help, -h</code></p></td><td style="text-align: left;"><p>Help output for the <code>init</code> command.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--plugins</code> (string)</p></td><td style="text-align: left;"><p>Name and optionally version of the plug-in to initialize the project with. Available plug-ins are <code>ansible.sdk.operatorframework.io/v1</code>, <code>go.kubebuilder.io/v2</code>, <code>go.kubebuilder.io/v3</code>, and <code>helm.sdk.operatorframework.io/v1</code>.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>--project-version</code></p></td><td style="text-align: left;"><p>Project version. Available values are <code>2</code> and <code>3-alpha</code>, which is the default.</p></td></tr></tbody></table>

`init` flags

# run

The `operator-sdk run` command provides options that can launch the Operator in various environments.

## bundle

The `run bundle` subcommand deploys an Operator in the bundle format with Operator Lifecycle Manager (OLM).

<table><caption><code>run bundle</code> flags</caption><colgroup><col style="width: 25%" /><col style="width: 75%" /></colgroup><thead><tr class="header"><th style="text-align: left;">Flag</th><th style="text-align: left;">Description</th></tr></thead><tbody><tr class="odd"><td style="text-align: left;"><p><code>--index-image</code> (string)</p></td><td style="text-align: left;"><p>Index image in which to inject a bundle. The default image is <code>quay.io/operator-framework/upstream-opm-builder:latest</code>.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--install-mode &lt;install_mode_value&gt;</code></p></td><td style="text-align: left;"><p>Install mode supported by the cluster service version (CSV) of the Operator, for example <code>AllNamespaces</code> or <code>SingleNamespace</code>.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>--timeout &lt;duration&gt;</code></p></td><td style="text-align: left;"><p>Install timeout. The default value is <code>2m0s</code>.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--kubeconfig</code> (string)</p></td><td style="text-align: left;"><p>Path to the <code>kubeconfig</code> file to use for CLI requests.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>n</code>, <code>--namespace</code> (string)</p></td><td style="text-align: left;"><p>If present, namespace in which to run the CLI request.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>-h</code>, <code>--help</code></p></td><td style="text-align: left;"><p>Help output for the <code>run bundle</code> subcommand.</p></td></tr></tbody></table>

`run bundle` flags

-   See [Operator group membership](../../operators/understanding/olm/olm-understanding-operatorgroups.xml#olm-operatorgroups-membership_olm-understanding-operatorgroups) for details on possible install modes.

## bundle-upgrade

The `run bundle-upgrade` subcommand upgrades an Operator that was previously installed in the bundle format with Operator Lifecycle Manager (OLM).

<table><caption><code>run bundle-upgrade</code> flags</caption><colgroup><col style="width: 25%" /><col style="width: 75%" /></colgroup><thead><tr class="header"><th style="text-align: left;">Flag</th><th style="text-align: left;">Description</th></tr></thead><tbody><tr class="odd"><td style="text-align: left;"><p><code>--timeout &lt;duration&gt;</code></p></td><td style="text-align: left;"><p>Upgrade timeout. The default value is <code>2m0s</code>.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>--kubeconfig</code> (string)</p></td><td style="text-align: left;"><p>Path to the <code>kubeconfig</code> file to use for CLI requests.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>n</code>, <code>--namespace</code> (string)</p></td><td style="text-align: left;"><p>If present, namespace in which to run the CLI request.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>-h</code>, <code>--help</code></p></td><td style="text-align: left;"><p>Help output for the <code>run bundle</code> subcommand.</p></td></tr></tbody></table>

`run bundle-upgrade` flags

# scorecard

The `operator-sdk scorecard` command runs the scorecard tool to validate an Operator bundle and provide suggestions for improvements. The command takes one argument, either a bundle image or directory containing manifests and metadata. If the argument holds an image tag, the image must be present remotely.

<table><caption><code>scorecard</code> flags</caption><colgroup><col style="width: 25%" /><col style="width: 75%" /></colgroup><thead><tr class="header"><th style="text-align: left;">Flag</th><th style="text-align: left;">Description</th></tr></thead><tbody><tr class="odd"><td style="text-align: left;"><p><code>-c</code>, <code>--config</code> (string)</p></td><td style="text-align: left;"><p>Path to scorecard configuration file. The default path is <code>bundle/tests/scorecard/config.yaml</code>.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>-h</code>, <code>--help</code></p></td><td style="text-align: left;"><p>Help output for the <code>scorecard</code> command.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>--kubeconfig</code> (string)</p></td><td style="text-align: left;"><p>Path to <code>kubeconfig</code> file.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>-L</code>, <code>--list</code></p></td><td style="text-align: left;"><p>List which tests are available to run.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>-n</code>, --namespace (string)</p></td><td style="text-align: left;"><p>Namespace in which to run the test images.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>-o</code>, <code>--output</code> (string)</p></td><td style="text-align: left;"><p>Output format for results. Available values are <code>text</code>, which is the default, and <code>json</code>.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>-l</code>, <code>--selector</code> (string)</p></td><td style="text-align: left;"><p>Label selector to determine which tests are run.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>-s</code>, <code>--service-account</code> (string)</p></td><td style="text-align: left;"><p>Service account to use for tests. The default value is <code>default</code>.</p></td></tr><tr class="odd"><td style="text-align: left;"><p><code>-x</code>, <code>--skip-cleanup</code></p></td><td style="text-align: left;"><p>Disable resource cleanup after tests are run.</p></td></tr><tr class="even"><td style="text-align: left;"><p><code>-w</code>, <code>--wait-time &lt;duration&gt;</code></p></td><td style="text-align: left;"><p>Seconds to wait for tests to complete, for example <code>35s</code>. The default value is <code>30s</code>.</p></td></tr></tbody></table>

`scorecard` flags

-   See [Validating Operators using the scorecard tool](../../operators/operator_sdk/osdk-scorecard.xml#osdk-scorecard) for details about running the scorecard tool.
