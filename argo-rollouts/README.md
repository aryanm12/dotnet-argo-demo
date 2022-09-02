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