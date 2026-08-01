---
name: Build and deploy a companion workflow
description: Create a project, build a workflow graph of nodes and edges, and deploy it (v2 Builder).
api: openapi/outrival-v2-openapi-original.json
operations: [WorkflowProjectController_createProject, WorkflowController_createWorkflow, WorkflowController_addNode, EdgeController_createEdge, WorkflowDeploymentController_createWorkflowDeployment]
---

# Build and deploy a companion workflow

Authenticate with the `X-API-Key` header. Base URL: `https://api.outrival.com` (v2 paths).

## Steps

1. **Create a project** — `POST /rest/v2/projects`
   (`WorkflowProjectController_createProject`). Capture the project `id`.
2. **Create a workflow** — `POST /rest/v2/workflows` (`WorkflowController_createWorkflow`)
   referencing the project.
3. **Add nodes** — `POST /rest/v2/workflows/{id}/nodes` (`WorkflowController_addNode`) for each
   step; configure a node's modality via `PATCH /rest/v2/nodes/{nodeId}/voice|sms|chat`.
4. **Connect nodes** — `POST /rest/v2/edges` (`EdgeController_createEdge`) to wire node handles.
5. **Deploy** — `POST /rest/v2/deployments`
   (`WorkflowDeploymentController_createWorkflowDeployment`); list deployments with
   `GET /rest/v2/projects/{id}/deployments`.

## Notes

- List endpoints paginate: offset style (`page`, `take`, `order`) for projects/workflows/nodes/edges;
  cursor style (`startingAfter`, `limit`) for ai-chats sessions/logs. See
  `conventions/outrival-conventions.yml`.
- Inspect conversation sessions/logs under `GET /rest/v2/ai-chats/...` once the workflow runs.
