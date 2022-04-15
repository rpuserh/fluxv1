# flux v1 kustomize manifest-generation POC

#### Flux v1 install
```
fluxctl install --git-url=git@github.com:rpuserh/fluxv1 --git-email=rpuserh@gmail.com --git-branch=main --namespace=flux --git-path=stage --manifest-generation=true | kubectl apply -f -
helm repo add fluxcd https://charts.fluxcd.io
helm upgrade -i helm-operator fluxcd/helm-operator     --namespace flux     --set helm.versions=v3
export FLUX_FORWARD_NAMESPACE=flux
fluxctl identity 
```

#### Problems during POC
  - Nested folders are not working unless included in kustomizatio
  - When changing yaml in repo like resource namespace new resources will be created old resources will not be deleted
  - some of advances kustomize resource definitions won't work: ex.
```
transformers:
- |-
  apiVersion: builtin
  kind: PrefixSuffixTransformer
  metadata:
    name: releaseNameprefixer
  prefix: stage-
  fieldSpecs:
  - path: spec/releaseName
```
