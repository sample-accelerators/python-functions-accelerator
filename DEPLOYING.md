# Deploying to Kubernetes

> NOTE: The provided `config/workload.yaml` file uses the Git URL for this sample. When you want to modify the source, you must push the code to your own Git repository and then update the `spec.source.git` information in the `config/workload.yaml` file.

## Using the Templates

You may use the [Func CLI](https://github.com/knative-sandbox/kn-plugin-func) locally or use Supply Chain for Tanzu Application Platform.

A default builder is provided to you here:
```
builders:
  default: us.gcr.io/daisy-284300/kn-fn/builder:0.0.6
```

## Deploying to Kubernetes as a TAP workload with Tanzu CLI

You need to select `Include TAP deployment resources` when using this Accelerator templates for the steps below to function.

When you are done developing your app, you can simply deploy it using:

```
tanzu apps workload apply -f config/workload.yaml
```

If you would like deploy the code from your local working directory you can use the following command:

```
tanzu apps workload create functions-accelerator -f config/workload.yaml \
  --local-path . \
  --source-image <REPOSITORY-PREFIX>/functions-accelerator-source \
  --type web
```

## Accessing the app deployed to your cluster

If you don't have `curl` installed it can be installed using downloads here: https://curl.se/download.html

Determine the URL to use for the accessing the app by running:

```
tanzu apps workload get functions-accelerator
```

To access the deployed app open the URL shown in your browser.

This depends on the TAP installation having DNS configured for the Knative ingress.