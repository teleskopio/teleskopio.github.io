---
title: teleskopio with kind
date: 2026-01-05
tags: ["docker", "kind", "howtos"]
---

#### [Run](#run-2)

#### [Setup kind](#setup-kind-2)

#### [Deploy a Pod](#deploy-a-pod-2)

#### [Multiselect](#multiselect-2)

#### [Scale Resources](#scale-resources-2)

#### [Cronjob](#cronjob-2)

#### [Cordon and Drain](#cordon-and-drain-2)

#### [Theme and Font](#theme-and-font-2)

Let's explore the features of `teleskopio`.

Requirements:

- Kubernetes clusters of any version.
- `kubeconfig` of the cluster.

That's it-we only need access to the cluster to run `teleskopio`.

In this example I'm going to use [`kind`](https://kind.sigs.k8s.io/), it's a very popular tool in the Kubernetes world (by the way `kind` is used in the Kubernetes e2e pipelines).

> kind is a tool for running local Kubernetes clusters using Docker container “nodes”.
> kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

#### Setup kind

Let's create a simple cluster.

```shell
> kind create cluster
Creating cluster "kind" ...
 ✓ Ensuring node image (kindest/node:v1.35.0) 🖼
 ✓ Preparing nodes 📦
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind

Have a nice day! 👋
```

Now copy the contents of the `~/.kube/config` file or ensure the `KUBECONFIG` environment variable points to the correct location.

Run `teleskopio config`, which prints a sample config to stdout.

Generate a user with hashed password and add it to the `config.yaml`.

```shell
> htpasswd -nbB admin MySecret12345
$ admin:$2y$05$GUduJJ9FF.WA8J4zl4vJ4OfKuoszAPJ2iqMt6BcPoQ8kZ3wGy..n.
```

#### Run

Run `teleskopio --config=./config.yaml`.

<video controls="" loop="" autoplay="off" muted="" playsinline="" aria-labelledby="login to cluster" src="./login.mp4"></video>

If everything goes well, you'll see the login screen and can use the `user/pass` from the `config.yaml`.

#### Deploy a pod

Let's deploy a pod to our cluster. Double click on pod. Check pod logs.

<video controls="" loop="" autoplay="none" muted="" playsinline="" aria-labelledby="open pod resource" src="deploy-pod.mp4"></video>

#### Multiselect

Now select a bunch of pods and delete them.

<video controls="" loop="" autoplay="none" muted="" playsinline="" aria-labelledby="delete pod resource" src="delete-pods.mp4"></video>

#### Scale Resources

Let's scale a deployment. Any resource that supports scaling can be scaled.

<video controls="" loop="" autoplay="none" muted="" playsinline="" aria-labelledby="scale resources" src="scale.mp4"></video>

#### Cronjob

You can trigger cronjob.

<video controls="" loop="" autoplay="none" muted="" playsinline="" aria-labelledby="cronjobs" src="cronjobs.mp4"></video>

#### Cordon and Drain

You can cordon or drain node(s).

<video controls="" loop="" autoplay="none" muted="" playsinline="" aria-labelledby="cordon and drain" src="cordon.mp4"></video>

#### Theme and Font

Another cool feature is font and theme.

<video controls="" loop="" autoplay="none" muted="" playsinline="" aria-labelledby="theme and font" src="change-theme-font.mp4"></video>

That's a brief overview of the `teleskopio` features.

Feel free to try it!
