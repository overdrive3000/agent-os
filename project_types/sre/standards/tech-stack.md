# Default SRE Tech Stack Template

## Cloud & Infrastructure
- **Cloud Provider:** [AWS / GCP / Azure / ...]
- **Regions:** [List primary regions]
- **Resource Provisioning:** Terraform (preferred) with remote state in [Backend]

## Runtime & Orchestration
- **Primary Runtime:** [Kubernetes / ECS / VMs]
- **Workload Types:** [Stateless services, batch jobs, etc.]
- **Autoscaling Strategy:** [HPA, Karpenter, ASG policies]

## Deployment & Automation
- **CI/CD Pipelines:** [GitHub Actions / GitLab CI / ArgoCD]
- **Release Strategy:** [Blue/Green, Canary, Rolling]
- **Secrets Management:** [AWS Secrets Manager, Vault, SSM]

## Observability
- **Metrics:** [Prometheus, CloudWatch]
- **Logging:** [ELK, Loki, Cloud provider]
- **Tracing:** [Tempo, X-Ray, Jaeger]
- **Alert Routing:** [PagerDuty, Opsgenie]

## Compliance & Security
- **Policy Enforcement:** [OPA/Gatekeeper, Terraform Cloud Policies]
- **Vulnerability Scanning:** [Trivy, Grype]
- **Access Management:** [IAM Roles, SSO Provider]

## Disaster Recovery
- **Backups:** [Service + cadence]
- **DR Strategy:** [Pilot light, warm standby, multi-region active/active]
- **Testing Cadence:** [Monthly/Quarterly]

Customize each section to reflect the actual tooling for this project before running specs or tasks.
