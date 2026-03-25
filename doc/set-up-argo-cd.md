## TODO / QUESTIONS
- [ ] Where does config lives?
- [ ] How to install Argo in cluster?
- [ ] How to to have multiple envs (dev / prod)?

## DONE

## WITHDRAWN

## References
- [Argo cd helm chard repo](https://github.com/argoproj/argo-helm/tree/main/charts/argo-cd)

## Plan

## Exploration

### Helm vs Kustomize

These two tools are not competing — they complement each other. Kustomize shines for
patching and overlaying configs; Helm shines for installing off-the-shelf apps.

#### Questions
- [ ] Helm
  - [ ] Where does helm pulls config for of the shell apps?
  - [ ] Where does helm pulls config for of the shell apps?
  - [ ] How does updating helm itself works?
  - [ ] How does updating apps installed via helm works?
  - [ ] Can all the operations above be handle via git-ops and argo cd?
- [ ] Kustomize
  - [ ] So we grab the manifest / configuration from helm and customize them with
        with kustomize?
- [ ] Helm + kustomize
  - [ ] Is it a fair assumption that we would use go templating when working with
        helm apps and later to create multiple envs (dev / prod) we are on a better
        position to use kustomize?
  
#### Helm — https://helm.sh/docs/topics/architecture/

Think of Helm as apt/brew for Kubernetes. It bundles everything an app needs into a
Chart (versioned, templated YAML). You install a chart with a `values.yaml` to
configure it.

- Great for 3rd-party software: Prometheus, cert-manager, Argo CD itself
- Has a package ecosystem — point at a repo and install
- Downside: Go templating can get complex, and you can only configure what the chart
  author exposed as a value

#### Questions
- [ ] So I can configure helm charts with go templates and or kustomize and or
      the values.yaml file?
- [ ] Show me examples of go templates and how can it get complex

#### Kustomize — https://kubectl.docs.kubernetes.io/guides/introduction/kustomize/

Think of Kustomize as git patches for YAML. You start from a base (your own or
upstream) and layer overlays on top. No templating language — pure YAML.

- Great for customizing upstream manifests without forking them
- Native to `kubectl` — `kubectl apply -k` just works
- Downside: no package ecosystem, you manage upstream manifest URLs yourself

#### Questions
- [ ] Can the downside be mitigated with the use of source control?

### How Argo CD relates — https://argo-cd.readthedocs.io/en/stable/operator-manual/installation/

The official Argo CD docs list both Kustomize and Helm as supported installation
methods. Once Argo CD is running, it natively understands both — you can mix them
per-app.

Two places these tools apply:

1. Bootstrapping Argo CD itself — installing it into the cluster. You can use
   Helm (`helm install`), Kustomize (a `kustomization.yaml` wrapping the official
   install manifest), or plain `kubectl apply`.

2. Managing your apps with Argo CD — once running, Argo CD can deploy apps using
   Helm, Kustomize, or plain YAML, per app.

#### Questions
- [ ] What would be the best installation option? Let's do some tradeoff analysis

### Questions

- How does the App of Apps / ApplicationSet pattern work?
- What does a typical repo structure look like for a Kustomize-based GitOps setup?
- How does Argo CD watch Git and sync to the cluster?
- What apps do we actually want to deploy? (shapes all of the above)
