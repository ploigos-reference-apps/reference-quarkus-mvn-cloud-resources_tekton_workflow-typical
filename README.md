# reference-quarkus-mvn-cloud-resources (Tekton) (Workflow: Standard)
The cloud resources for the [reference-quarkus-mvn_tekton_workflow-standard](http://gitea.tssc.rht-set.com/ploigos-reference-applications/reference-quarkus-mvn_tekton_workflow-standard) application.

## Install

### 0. Prerequisite

* TODO

### 1. Deploy Ploigos Workflow
Since Tekton is a purly Kubernetes based workflow runner service its entire configuration can be
installed with Helm.

```bash
WORKFLOW_NAMESPACE=
helm dependency update charts/reference-quarkus-mvn-workflow

helm secrets upgrade --install \
    reference-quarkus-mvn-workflow ./charts/reference-quarkus-mvn-workflow \
    -f charts/reference-quarkus-mvn-workflow/values.yaml \
    -f charts/reference-quarkus-mvn-workflow/secrets.yaml \
    --namespace ${WORKFLOW_NAMESPACE} \
    --render-subchart-notes
```

### 2. Configure Source Control Service webhook

1. Configure your Source Control Service repository hosting your application to send Webhook events
to the EventListener Route:
    * HTTP method: POST
    * POST Content Type: application/json
    * Trigger On:
      - Repository Events
        * Push
      - Issue Events
        * Pull Request
        * Pull Request Synchronized
    * Branch filter
      - `main`
