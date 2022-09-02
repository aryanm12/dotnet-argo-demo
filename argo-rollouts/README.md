Argo Rollouts:
--------------

Create a rollouts yaml for using canary deployment:
---------------------------------------------------

check: kubernetes-manifests/hello.rollouts.yaml

spec:
  replicas: 5
  strategy:
    canary:
      steps:
      - setWeight: 20
      - pause: {}
      - setWeight: 40
      - pause: {duration: 10}
      - setWeight: 60
      - pause: {duration: 10}
      - setWeight: 80
      - pause: {duration: 10}

Configure the service to use the rollouts yaml:
-----------------------------------------------

check: kubernetes-manifests/hello.rollouts.service.yaml


# Push the Code in the Git Repo and sync using Argo CD

```
Initial creations of any Rollout will immediately scale up the replicas to 100% (skipping any canary upgrade steps, analysis, etc...) since there was no upgrade that occurred.

The Argo Rollouts kubectl plugin allows you to visualize the Rollout, its related resources (ReplicaSets, Pods, AnalysisRuns), and presents live state changes as they occur. To watch the rollout as it deploys, run the get rollout --watch command from plugin:
```


Get the rollout status:
-----------------------

kubectl argo rollouts get rollout dotnet-hello-world-rollouts -n dotnet-hello-world --watch


Updating a Rollout:
-------------------

# Update the image tag

Update the image version in the kubernetes-manifests/hello.rollouts.service.yaml to "2.0.0"

commit and push the code