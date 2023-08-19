# Package Feeds

The binary produced by [cmd/scheduled-feed/main.go](cmd/scheduled-feed/main.go) can be used to monitor various
package repositories for changes and publish data to external services for further processing.

Additionally, the repo contains a few subprojects to aid in the analysis of these open source packages, in particular to look for malicious software.

These are:

[Feeds](./pkg/feeds/) to watch package registries (PyPI, NPM, etc.) for changes to packages
and to make that data available via a single standard interface.

[Publisher](./pkg/publisher/) provides the functionality to push package details from feeds towards
external services such as GCP Pub/Sub. Package details are formatted inline with a versioned
[json-schema](./package.schema.json).

This repo used to contain several other projects, which have since been split out into
[github.com/khulnasoft-lab/package-analysis](https://github.com/khulnasoft-lab/package-analysis).

The goal is for all of these components to work together and provide extensible, community-run
infrastructure to study behavior of open source packages and to look for malicious software.
We also hope that the components can be used independently, to provide package feeds or runtime
behavior data for anyone interested.

# Configuration

A YAML configuration file can be provided with the following format:

```
feeds:
- type: pypi
- type: npm
- type: goproxy
- type: rubygems
- type: crates

publisher:
  type: 'gcp_pubsub'
  config:
    url: "gcppubsub://foobar.com"

http_port: 8080

poll_rate: 5m

timer: false
```
