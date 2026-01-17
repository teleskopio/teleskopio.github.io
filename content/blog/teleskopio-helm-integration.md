---
title: teleskopio helm integration
date: 2026-01-17
tags: ["kind", "helm", "howtos"]
---

#### [Helm](#helm-2)

#### [Under the hood](#under-the-hood-2)

Hey! Hope you're doing fine.

The `teleskopio` has released a new version with Helm integration.
In this article, I'll explain how that feature was developed.

We'll test it on a kind cluster.
Let's create a simple cluster. In the previous post, you can find how to set up a cluster with kind.

#### Helm

Run `teleskopio --config=./config.yaml`.

<video controls="" loop="" autoplay="off" muted="" playsinline="" aria-labelledby="login to cluster" src="./helm-integration.mp4"></video>

In this video we've run a bunch of `helm install/uninstall` commands in another terminal. In the `teleskopio` web ui we're able to open manifests of `helm` release by double click on the release column.

#### Under the hood

From the backend side the realization is pretty simple and build on top of helm golang SDK.
We have a kubernetes client initialized and with what client we can initialize the helm client.

Here is an example:

```go
flags := genericclioptions.NewConfigFlags(false)
// Spoof kube config on the fly
flags.WrapConfigFn = func(_ *rest.Config) *rest.Config {
    return r.GetCluster(req.Server).RestConfig
}
actionConfig := new(action.Configuration)
err := actionConfig.Init(flags, ns, "secret", slog.Default().Info)
// Handle error

list := action.NewList(actionConfig)
list.All = true

rels, err := list.Run()
// rels is a helm releases slice
```

After list `helm` releases we're create an kubernetes shared index informers and watch `Secret` resources.

> A Kubernetes shared index informer is a mechanism in the client-go library for efficiently watching, listing, and caching Kubernetes resources, with the added ability to create custom indexes for fast data retrieval. It is the foundation for building Kubernetes controllers and operators.

That's because of `helm` nature.

> Helm stores release metadata, including chart data and values, in Kubernetes Secrets by default.

In this `teleskopio` version the `helm` backend hardcoded as `Secret`, maybe we'll add more backends (`ConfigMap`, `sql` etc) in the future.

If you want know more feel free to dig `teleskopio` source code.

That's a brief overview of the `teleskopio` features.

Happy coding!
