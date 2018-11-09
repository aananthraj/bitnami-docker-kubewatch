[![CircleCI](https://circleci.com/gh/bitnami/bitnami-docker-kubewatch/tree/master.svg?style=shield)](https://circleci.com/gh/bitnami/bitnami-docker-kubewatch/tree/master)

# What is Kubewatch?

> Kubewatch is a Kubernetes watcher that currently publishes notification to Slack.
> Run it in your k8s cluster, and you will get event notifications in a slack channel.

[https://github.com/bitnami-labs/kubewatch]

# TL;DR;

```bash
$ docker run --name kubewatch bitnami/kubewatch:latest
```

# Why use Bitnami Images?

* Bitnami closely tracks upstream source changes and promptly publishes new versions of this image using our automated systems.
* With Bitnami images the latest bug fixes and features are available as soon as possible.
* Bitnami containers, virtual machines and cloud images use the same components and configuration approach - making it easy to switch between formats based on your project needs.
* Bitnami images are built on CircleCI and automatically pushed to the Docker Hub.
* All our images are based on [minideb](https://github.com/bitnami/minideb) a minimalist Debian based container image which gives you a small base container image and the familiarity of a leading linux distribution.
* Bitnami container images are released daily with the latest distribution packages available.

[![Anchore Image Overview](https://anchore.io/service/badges/image/13ca668951dbeb979d59c01d20a94adb517a8bb1661dfd3e1c4473719b4645bd)](https://anchore.io/image/dockerhub/bitnami%2Fkubewatch%3Alatest#security)

> The image overview badge contains a security report with all open CVEs. Click on 'Show only CVEs with fixes' to get the list of actionable security issues.

# How to deploy Kubewatch in Kubernetes?

Deploying Bitnami applications as Helm Charts is the easiest way to get started with our applications on Kubernetes. Read more about the installation in the [Bitnami Kubewatch Chart GitHub repository](https://github.com/bitnami/charts/tree/master/upstreamed/kubewatch).

Bitnami containers can be used with [Kubeapps](https://kubeapps.com/) for deployment and management of Helm Charts in clusters.

# Why use a non-root container?

Non-root container images add an extra layer of security and are generally recommended for production environments. However, because they run as a non-root user, privileged tasks are typically off-limits. Learn more about non-root containers [in our docs](https://docs.bitnami.com/containers/how-to/work-with-non-root-containers/).

# Supported tags and respective `Dockerfile` links

> NOTE: Debian 8 images have been deprecated in favor of Debian 9 images. Bitnami will not longer publish new Docker images based on Debian 8.

Learn more about the Bitnami tagging policy and the difference between rolling tags and immutable tags [in our documentation page](https://docs.bitnami.com/containers/how-to/understand-rolling-tags-containers/).


* [`0-ol-7`, `0.0.4-ol-7-r125` (0/ol-7/Dockerfile)](https://github.com/bitnami/bitnami-docker-kubewatch/blob/0.0.4-ol-7-r125/0/ol-7/Dockerfile)
* [`0-debian-9`, `0.0.4-debian-9-r97`, `0`, `0.0.4`, `0.0.4-r97`, `latest` (0/debian-9/Dockerfile)](https://github.com/bitnami/bitnami-docker-kubewatch/blob/0.0.4-debian-9-r97/0/debian-9/Dockerfile)

Subscribe to project updates by watching the [bitnami/kubewatch GitHub repo](https://github.com/bitnami/bitnami-docker-kubewatch).

# Configuration

## Environment variables

The Kubewatch instance can be customized by specifying the below environment variables on the first run:

- `KW_SLACK_CHANNEL`: Slack channel. No defaults.
- `KW_SLACK_TOKEN`: Slack token. No defaults.
- `KW_HIPCHAT_ROOM`: HipChat room. No defaults.
- `KW_HIPCHAT_TOKEN`: HipChat token. No defaults.
- `KW_HIPCHAT_URL`: HipChat URL. No defaults.
- `KW_MATTERMOST_CHANNEL`: Mattermost channel. No defaults.
- `KW_MATTERMOST_URL`: Mattermost URL. No defaults.
- `KW_MATTERMOST_USERNAME`: Mattermost username. No defaults.
- `KW_FLOCK_URL`: Flock URL. No defaults.
- `KW_WEBHOOK_URL`: WEBHOOK URL. No defaults.

## Configuration file

In addition to the above environment variables, you can mount your custom configuration file via docker volume or kubernetes config map.

For example, if you want to receive slack notifications for every change in every kubernetes resource you can do the following:

1. Write this config file and name it *kubewatch.yaml*

```
handler:
  slack:
    token: YOUR_SLACK_TOKEN
    channel: YOUR_SLACK_CHANNEL
resource:
  deployment: true
  replicationcontroller: true
  replicaset: true
  daemonset: true
  services: true
  pod: true
  job: true
  persistentvolume: true
  namespace: true
  secret: true
  ingress: true
```

2. Launch the Bitnami Kubewatch container mounting the previous configuration file:

```bash
$ docker run --name kubewatch \
  --volume path/to/your/kubewatch.yaml:/opt/bitnami/kubewatch/.kubewatch.yaml \
  bitnami/kubewatch:latest
```

or using the following docker-compose file:

```yaml
version: '2'

services:
  kubewatch:
    image: bitnami/kubewatch:latest
    volumes:
      -  ./path/to/your/kubewatch.yaml:/opt/bitnami/kubewatch/.kubewatch.yaml
```

# Contributing

We'd love for you to contribute to this container. You can request new features by creating an [issue](https://github.com/bitnami/bitnami-docker-kubewatch/issues), or submit a [pull
request](https://github.com/bitnami/bitnami-docker-kubewatch/pulls) with your contribution.

# Issues

<!-- If you encountered a problem running this container, you can file an [issue](https://github.com/bitnami/bitnami-docker-kubewatch/issues). For us to provide better support, be sure to include the following information in your issue: -->

- Host OS and version
- Docker version (`docker version`)
- Output of `docker info`
- Version of this container
- The command you used to run the container, and any relevant output you saw (masking any sensitive information)

# License
Copyright 2018 Bitnami

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
