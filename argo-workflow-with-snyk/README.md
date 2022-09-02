Argo Workflow:
--------------

# Create Argo workflow for building and pushing the docker image:
-----------------------------------------------------------------

argo --namespace argo submit argo-hello-world-dotnet-workflow.yaml


Snyk Container - Tool to test docker images:
--------------------------------------------

Getting started with Snyk Container:
------------------------------------

- Create a Snyk Account: https://docs.snyk.io/getting-started/create-a-snyk-account

- Get the Snyk token from your account

- Create Snyk secret in Kubernetes under Argo Workflow Namespace

export SNYK_TOKEN=xxxxxxxxxxxxxxxxxxx

kubectl -n argo create secret generic snyk-token --from-literal=snyktoken=$SNYK_TOKEN

- Create a workflow template:

    - name: test-image-snyk
    container:
      image: snyk/snyk:dotnet
      command: [snyk]
      args:
      - container
      - test
      - aryanmohan/dotnet-argo-demo:2.0.0
      env:
      - name: SNYK_TOKEN
        valueFrom:
          secretKeyRef:
            name: snyk-token
            key: snyktoken
      volumeMounts:
      - name: snyk-vol
        mountPath: "/secret/snyk"

- Call the template from the main dag: 
    reference: argo-hello-world-dotnet-workflow.yaml

- Check the results on the logs of the above workflow