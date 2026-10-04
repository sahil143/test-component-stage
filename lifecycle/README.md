# New Component lifecycle demo

Namespace: `sbudhwar-1-tenant` only.

Components `lifecycle-api` and `lifecycle-worker` each have versions `v1` and `v2`,
tracking `codex/lifecycle-v1` and `codex/lifecycle-v2`. Their images contain
`/version.txt` with the component identity and semantic version.

Groups `lifecycle-v1` and `lifecycle-v2` each include both components at the
matching version. Each group has snapshot smoke validation followed by a gate.
Successful push snapshots trigger tenant-only ReleasePlans with the same names.
The release pipeline records the release, plan and snapshot references; it is a
lifecycle demo and does not publish a production release.

Build configuration is requested through the new Component actions API.
Merge the generated Konflux PRs into their respective lifecycle branches.
The existing main branch and its legacy pipeline files remain separate.

Initial provisioning: `oc create -n sbudhwar-1-tenant -f lifecycle/manifests/resources.yaml`.
The Component actions are one-shot requests, so do not repeatedly apply them.

Observe:
```sh
oc get components.konflux-ci.dev,componentgroups.appstudio.redhat.com -n sbudhwar-1-tenant
oc get pipelineruns,snapshots,releases -n sbudhwar-1-tenant
```
