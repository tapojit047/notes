# Helm:
### Package Manager: 
- A package manager is a software tool that manages the installation and removal of software packages on a computer. Package managers automate the process of installing, upgrading, configuring and removing software, and they can also help to resolve dependencies between different software packages.
- Examples of package managers include apt for Debian and Ubuntu Linux distributions, yum for Red Hat and Fedora Linux distributions, and Homebrew for macOS. There are also cross-platform package managers like npm for JavaScript, pip for Python, and gem for Ruby.

## Notes:
- A Chart is a Helm package. It contains all of the resource definitions necessary to run an application, tool, or service inside of a Kubernetes cluster.
- A Release is an instance of a chart running in a Kubernetes cluster. One chart can often be installed many times into the same cluster.

# Helm: 
- Helm installs charts into Kubernetes, creating a new release for each installation. And to find new charts, you can search Helm chart repositories.

## Charts:
- Helm uses a packaging format called charts. A chart is a collection of files that describe a related set of Kubernetes resources.
- 