# Understand Cloud Foundry

## Concepts/Applications

1. BOSH
2. cf CLI
3. fly CLI
4. Garden
5. Cell
6. Stemcell
7. Buildpack

### BOSH

Does something with releases.  Is it a program that an operator runs locally to control releases?

### cf CLI

Administer Cloud Foundry.  You can manage apps, services, orgs, spaces, domains, routes, buildpacks, plug-ins, users.

### fly CLI

Command line tool used to control concourse.ci, a pivotal build pipeline manager

### Garden

API that creates and manages containers that app instances run on.  Garden Windows uses IronFrame to implement containerization on Windows.  Garden Windows achieves container isolation of file system, disk usage, network usage, and memory usage.

### Cell

This looks like a container host and runs all the required services that Cloud Foundry needs to operate.  This includes Garden, Containerizer, Metron Agent, BOSH Agent, Consul Client, Cell Rep.

### Stemcell

I'm assuming this is a base image that cells are created from.

## [Including a .NET application in Cloud Foundry](http://engineering.pivotal.io/post/dotnet-quick-intro/)

### Pre-requisites

1. An existing Cloud Foundry installation
2. One Windows cell using the lastest compatible Diego Windows and Garden Windows MSIs
3. Git for Windows
4. The latest Cloud Foundry CLI

### Deploying

1. Clone your repo locally
2. ```cf push``` your application

### Installing Diego Enabler CLI plugin and deploying

```
$ cf add-plugin-repo CF-Community http://plugins.cloudfoundry.org/
$ cf install-plugin Diego-Enabler -r CF-Community
$ cf push my-app -s windows2012R2 -b binary_buildpack -p --no-start ./my-app/ViewEnvironment/
$ cf enable-diego my-app
$ cf start my-app
```

### Notes

Windows application rely on binary_buildpack, but I don't know what binary_buildpack is.

Also, we should publish (build?) the application in VS and then push the folder you've published to, rather than the root of the repo.

