# Deploying

## Pre-Requisites
- [curl](https://curl.se/download.html)
- [pack](https://buildpacks.io/docs/tools/pack/) >= `0.23.0`
- [func](https://github.com/knative-sandbox/kn-plugin-func/blob/main/docs/installing_cli.md)

## Building your function

You can build your function using our provided builder:
```
pack build <MY-FUNCTION-NAME> --path . --builder us.gcr.io/daisy-284300/kn-fn/builder:0.0.6
```

## Local Deployment

### Docker

This assumes you have Docker Desktop properly installed and running.

With Docker Desktop running, authenticated, and the ports (default `8080`) available:

```
docker run -it --rm -p 8080:8080 sample-java
```

## Testing
After deploying your function, you can interact with our templates by doing:
- Single function definition: `curl -X POST localhost:8080`
- Multiple function definitions: `curl -H "Content-Type: application/json" -X POST localhost:8080/hello`
- - where `hello` as a path invokes your function's definition

With our templates, you should see some HTML or sample text returned indicating a success.

## TAP Deployment - Alpha
### Deploying to Kubernetes

> NOTE: The provided `config/workload.yaml` file uses the Git URL for this sample. When you want to modify the source, you must push the code to your own Git repository and then update the `spec.source.git` information in the `config/workload.yaml` file.


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

## Interacting with Tanzu Application Platform

Determine the URL to use for the accessing the app by running:

```
tanzu apps workload get functions-accelerator
```

To access the deployed app open the URL shown in your browser.

This depends on the TAP installation having DNS configured for the Knative ingress.