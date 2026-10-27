# Public GitHub portfolio review

Reviewed October 27, 2026, using the [public profile](https://github.com/thupeshkumar) and repository metadata/file trees from GitHub. Repository changes after this review may change the findings. Non-fork status is a selection signal, not proof of sole authorship. Training projects can use upstream workloads; retain attribution and distinguish your deployment work from application authorship.

## Selected projects

### 1 Multi-cloud project

[Repository](https://github.com/thupeshkumar/multi-cloud-project)

The strongest overall DevOps narrative: provider modules, a small understandable Python controller, simulated tests, monitoring and separate recovery tooling. The replacement README emphasizes code, operating constraints and evidence rather than broad availability claims.

Evidence inspected: `terraform/main.tf`, the Azure module, `failover/failover.py`, `tests/test_failover.py`, monitoring Compose configuration, `.github/workflows/validate.yml`, `VALIDATION.md`, `SETUP.md` and DR documentation.

Follow-up fixes:

- Reconcile `SETUP.md`'s East US/B1s configuration with the West US 2/D2als_v7 module. The replacement README calls out the discrepancy.
- Refresh dated validation notes: the October 22 file says no provider lock file was generated, but the current tree contains one. Keep historical results dated instead of silently converting them into new test results.
- Remove the tracked Python bytecode cache in a separate cleanup commit and ignore future caches.
- Attach sanitized live failover and recovery evidence before claiming measured recovery, availability or cost results. Distinguish DNS update time from client recovery time.
- The GitHub Actions file runs Terraform checks; it does not currently run the Python controller tests. Adding those tests to CI is a useful next code change.

### 2 Terraform and Ansible AWS deployment

[Repository](https://github.com/thupeshkumar/mern-terraform-ansible)

Strong infrastructure and configuration-management material. Credit [TravelMemory](https://github.com/UnpredictablePrashant/TravelMemory) as the application source. Use this project to explain public/private tiers, security groups, systemd and the interaction between Terraform outputs and Ansible inventory.

Evidence inspected: README, inventory helper, Ansible configuration and variables, web playbook, security groups and repository tree.

Follow-up fixes:

- Correct `generate_inventory.sh`: it writes the wrong group-vars location relative to the active inventory and replaces placeholders destructively, which can leave stale addresses on subsequent runs.
- Resolve the frontend API path/port mismatch: the frontend points to public port 3001, but host firewall tasks do not explicitly allow it. A tested same-origin reverse proxy is preferable to broadly opening the application port.
- Enable verified SSH host-key checking, move example passwords into private overrides, review dependency support, and pin upstream application revisions for reproducibility.
- Replace screenshot instructions with actual evidence where available; the old README links to a missing architecture diagram. The new README uses an inline architecture sketch.
- Avoid copying the old troubleshooting suggestion to wipe database files. Investigate failed bootstrap/authentication without treating data deletion as routine recovery.

### 3 AKS microservices deployment

[Repository](https://github.com/thupeshkumar/mern-aks)

Adds Kubernetes depth to the portfolio: probes, resource requests/limits, service exposure, secrets references and persistent volumes. Credit [SampleMERNwithMicroservices](https://github.com/UnpredictablePrashant/SampleMERNwithMicroservices) for the upstream workload.

Evidence inspected: all five Kubernetes manifests, root README, deployment guide and repository tree.

Follow-up fixes:

- Replace the deployment guide's generic clone URL and missing individual screenshot links. The replacement root README supplies the correct clone URL and accurately identifies the evidence gap.
- Create a database-scoped application account instead of using the root credential shown in the lab guide.
- Add immutable image versions and test a delivery workflow before claiming CI/CD deployment automation.
- Add TLS, network isolation and recovery testing before presenting the setup as production-ready. Two application replicas do not remove the single MongoDB replica as a failure point.

## Other non-fork repositories reviewed

| Repository | Assessment |
| --- | --- |
| [Mern_Deployment](https://github.com/thupeshkumar/Mern_Deployment) | Useful monitoring screenshots and infrastructure/configuration files. The Azure pipeline selects Node 10 and calls a backend build command; validate the build contract and modernize the pipeline before presenting it as working delivery automation. Not selected over the clearer Terraform/Ansible example. |
| [Microservices-Task](https://github.com/thupeshkumar/Microservices-Task) | Good smaller containerization exercise. README contains shell wrapper text and escaped code fences; the Compose file has a shared bridge network but no explicit `depends_on` declarations despite a dependency-management claim. Worth polishing after the three main projects. |
| [lambda](https://github.com/thupeshkumar/lambda) | Small Boto3 EC2 start/stop function based on `Action` tags. README is an AWS Toolkit template. Needs scoped IAM, pagination/error handling, tests and actual scheduling configuration before claiming scheduled cost optimization. No cost savings inferred. |
| [multi-cloud-terraform](https://github.com/thupeshkumar/multi-cloud-terraform) | Additional provider modules and pipeline files. Overlaps with the stronger capstone; a workflow performs automatic apply on main. Validate working-directory, credentials, state and approval design before promoting it. |
| [Travelapp](https://github.com/thupeshkumar/Travelapp) | Containerized multi-environment application. README claims production readiness and references screenshot paths not present in the inspected tree. Needs evidence and clearer operational scope. |
| [MultienvApp](https://github.com/thupeshkumar/MultienvApp) | Similar travel-app content nested under `Thupesh_Travel_app`. Avoid pinning both this and Travelapp without a clear explanation of their different purposes. |
| [thupeshkumar](https://github.com/thupeshkumar/thupeshkumar) | Profile repository; replacement `ReadMe.md` prioritizes project links, role transition and explicit attribution over decorative statistics and unsupported claims. |

## Forks

Forks were inventoried but not audited as original implementation. Examples include `Blue-green-Deployment`, `flask_Practice`, `HeroVired_Capstone_MultiCloudDeploymentAndManagment` and `multi-cloud-capstone`. Forking is useful for study; feature a fork as a contribution only when you can point to your specific changes and retain upstream credit.

The machine-readable inventory is provided in `Repository_Inventory.json`. It records repository name, GitHub URL, fork status, default branch and tree commit where inspected. README replacements are limited to the three selected projects and the profile.
