Argo Workflow:
--------------

# Create Argo workflow for building and pushing the docker image:
-----------------------------------------------------------------

argo cluster-template create -n argo argo-workflow/workflow-templates/container-image.yaml

argo --namespace argo submit argo-hello-world-dotnet-workflow.yaml